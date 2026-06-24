# Backend principal: api-fila-virtual-transparente

Repositório: `schambeck/api-fila-virtual-transparente`.

O backend principal é o núcleo transacional da solução. Os componentes abaixo
são uma visão lógica proposta a partir das responsabilidades esperadas; nomes e
fronteiras devem ser ajustados quando confrontados com o código do repositório.

## Componentes

```mermaid
flowchart LR
    PROVIDER["api-whatsapp-provider-simulator"]
    ADMIN["ui-admin-fila-virtual"]
    MOBILE["app-fila-virtual-mobile"]

    subgraph API["api-fila-virtual-transparente"]
        WEBHOOK["WebhookController"]
        CONVERSATION["ConversationService"]
        QUEUE["QueueService"]
        RESERVATION["ReservationService"]
        NOTIFICATION["NotificationService"]
        PATIENT["PatientService"]
        CLIENT["WhatsAppProviderClient"]
        REPOS["repositories"]
    end

    DB[("PostgreSQL")]

    PROVIDER -->|"webhook HTTP"| WEBHOOK
    ADMIN -->|"HTTP"| QUEUE
    MOBILE -->|"HTTP"| PATIENT
    MOBILE -->|"HTTP"| QUEUE
    MOBILE -->|"HTTP"| RESERVATION

    WEBHOOK --> CONVERSATION
    CONVERSATION --> PATIENT
    CONVERSATION --> QUEUE
    CONVERSATION --> RESERVATION
    QUEUE --> NOTIFICATION
    RESERVATION --> NOTIFICATION
    NOTIFICATION --> CLIENT
    CLIENT -->|"HTTP"| PROVIDER

    CONVERSATION --> REPOS
    QUEUE --> REPOS
    RESERVATION --> REPOS
    PATIENT --> REPOS
    NOTIFICATION --> REPOS
    REPOS -->|"SQL"| DB
```

## Entrada na fila via WhatsApp

```mermaid
sequenceDiagram
    actor Paciente
    participant UI as ui-whatsapp-simulator
    participant Provider as api-whatsapp-provider-simulator
    participant Webhook as WebhookController
    participant Conversation as ConversationService
    participant Patient as PatientService
    participant Queue as QueueService
    participant DB as PostgreSQL
    participant Notification as NotificationService
    participant Client as WhatsAppProviderClient

    Paciente->>UI: Informa CPF/CNS e solicita entrada
    UI->>Provider: POST mensagem
    Provider->>Webhook: POST webhook
    Webhook->>Conversation: processar mensagem
    Conversation->>Patient: identificar ou cadastrar paciente
    Patient->>DB: consultar/salvar paciente
    Conversation->>Queue: solicitar entrada na fila
    Queue->>DB: criar QueueEntry WAITING
    Queue-->>Conversation: posição atual
    Conversation->>Notification: solicitar confirmação após commit
    Notification->>Client: enviar confirmação
    Client->>Provider: POST mensagem ativa
    Provider-->>Client: referência da mensagem
    Conversation-->>Webhook: processamento concluído
    Webhook-->>Provider: confirmação do webhook
    Provider-->>UI: mensagem disponível para polling
    UI-->>Paciente: exibe confirmação e posição
```

## Chamada do próximo paciente

```mermaid
sequenceDiagram
    actor Admin as Administrador UBS
    participant UI as ui-admin-fila-virtual
    participant Queue as QueueService
    participant DB as PostgreSQL
    participant Notification as NotificationService
    participant Client as WhatsAppProviderClient
    participant Provider as api-whatsapp-provider-simulator

    Admin->>UI: Seleciona "Chamar próximo"
    UI->>Queue: POST chamar próximo
    Queue->>DB: selecionar primeiro WAITING e alterar para CALLED
    DB-->>Queue: QueueEntry atualizada
    Queue-->>UI: paciente chamado
    Queue->>Notification: solicitar notificação após commit
    Notification->>Client: enviar mensagem com chave idempotente
    Client->>Provider: POST mensagem ativa
    Provider-->>Client: referência da mensagem
    UI-->>Admin: atualiza dashboard
```

A alteração de `WAITING` para `CALLED` deve ser atômica. Falha de notificação
não desfaz a transição já confirmada e deve permitir nova tentativa, conforme o
contrato de fila deste repositório.

## Estados de Conversation

Esta máquina de estados é **proposta**, pois o contrato local não define os
estados de conversa.

```mermaid
stateDiagram-v2
    [*] --> NEW
    NEW --> IDENTIFYING: primeira mensagem
    IDENTIFYING --> CHOOSING_SERVICE: paciente identificado
    IDENTIFYING --> CLOSED: cancelamento ou falha definitiva
    CHOOSING_SERVICE --> CONFIRMING: opção selecionada
    CONFIRMING --> QUEUED: entrada confirmada
    CONFIRMING --> CHOOSING_SERVICE: corrigir opção
    QUEUED --> CLOSED: fluxo concluído
    CHOOSING_SERVICE --> CLOSED: cancelamento
    CLOSED --> [*]
```

## Estados de QueueEntry

Os estados e transições seguem o contrato
`specifications/api-fila-virtual-transparente/queue-flow.md`.

```mermaid
stateDiagram-v2
    [*] --> WAITING: entrada na fila
    WAITING --> CALLED: próximo paciente
    WAITING --> CANCELLED: desistência
    CALLED --> IN_SERVICE: atendimento iniciado
    CALLED --> EXPIRED: tempo de resposta excedido
    CALLED --> CANCELLED: cancelamento
    IN_SERVICE --> COMPLETED: atendimento finalizado
    IN_SERVICE --> CANCELLED: cancelamento
    COMPLETED --> [*]
    CANCELLED --> [*]
    EXPIRED --> [*]
```
