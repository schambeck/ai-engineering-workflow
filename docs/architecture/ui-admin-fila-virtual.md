# Frontend administrativo: ui-admin-fila-virtual

Repositório: `schambeck/ui-admin-fila-virtual`.

O frontend administrativo permite à UBS visualizar a fila e executar comandos
autorizados. Os componentes são uma decomposição lógica **proposta**.

## Componentes

```mermaid
flowchart TB
    subgraph ADMIN["ui-admin-fila-virtual"]
        PAGE["QueueDashboardPage"]
        LIST["QueueList"]
        CARD["PatientQueueCard"]
        CALL["CallNextButton"]
        CLIENT["QueueApiClient"]
    end

    API["api-fila-virtual-transparente"]

    PAGE --> LIST
    LIST --> CARD
    PAGE --> CALL
    PAGE --> CLIENT
    CALL --> CLIENT
    CLIENT -->|"HTTP"| API
```

## Chamar próximo paciente

```mermaid
sequenceDiagram
    actor Admin as Administrador UBS
    participant Button as CallNextButton
    participant Client as QueueApiClient
    participant API as api-fila-virtual-transparente
    participant Provider as api-whatsapp-provider-simulator
    participant Page as QueueDashboardPage

    Admin->>Button: Clica em "Chamar próximo"
    Button->>Client: chamarProximo(queueId)
    Client->>API: POST comando
    API->>API: WAITING → CALLED em transação
    API-->>Client: paciente chamado e fila atualizada
    API->>Provider: POST notificação ativa
    Client-->>Page: atualizar estado do dashboard
    Page-->>Admin: destaca paciente chamado
```

## Fluxo de dados do dashboard

```mermaid
flowchart LR
    PAGE["QueueDashboardPage"] -->|"solicita dados"| CLIENT["QueueApiClient"]
    CLIENT -->|"HTTP GET"| API["api-fila-virtual-transparente"]
    API -->|"fila ordenada e resumo"| CLIENT
    CLIENT --> PAGE
    PAGE --> LIST["QueueList"]
    LIST --> CARD["PatientQueueCard"]
    PAGE --> CALL["CallNextButton"]
    CALL -->|"comando HTTP via client"| API
```

Atualização automática do dashboard por polling, SSE ou WebSocket é uma decisão
**futura**. Até sua definição, o diagrama assume carga inicial e atualização
após comandos.
