# Provider simulado: api-whatsapp-provider-simulator

Repositório: `schambeck/api-whatsapp-provider-simulator`.

O serviço simula a fronteira de um provedor WhatsApp. A decomposição abaixo é
**proposta** e evita acoplar o backend principal ao formato de um provedor real.

## Componentes

```mermaid
flowchart LR
    UI["ui-whatsapp-simulator"]
    BACKEND["api-fila-virtual-transparente"]

    subgraph PROVIDER["api-whatsapp-provider-simulator"]
        MESSAGE["MessageController"]
        STORE["ProviderMessageStore"]
        FORWARDER["WebhookForwarder"]
        POLLING["PollingController"]
    end

    UI -->|"HTTP POST"| MESSAGE
    MESSAGE --> STORE
    MESSAGE --> FORWARDER
    FORWARDER -->|"webhook HTTP"| BACKEND
    BACKEND -->|"HTTP: mensagem ativa"| MESSAGE
    POLLING --> STORE
    UI -->|"HTTP GET a cada 2 s"| POLLING
```

`ProviderMessageStore` pode ser inicialmente em memória no ambiente de
simulação. Persistência durável, retenção e concorrência são decisões a
confirmar no repositório do provider.

## Paciente envia mensagem

```mermaid
sequenceDiagram
    actor Paciente
    participant UI as ui-whatsapp-simulator
    participant Controller as MessageController
    participant Store as ProviderMessageStore
    participant Forwarder as WebhookForwarder
    participant Backend as api-fila-virtual-transparente

    Paciente->>UI: Digita e envia mensagem
    UI->>Controller: POST mensagem recebida
    Controller->>Store: registrar mensagem do paciente
    Controller->>Forwarder: encaminhar payload
    Forwarder->>Backend: POST webhook
    Backend-->>Forwarder: 2xx acknowledgment
    Controller-->>UI: mensagem aceita
```

## Backend envia mensagem ativa

```mermaid
sequenceDiagram
    participant Backend as api-fila-virtual-transparente
    participant Controller as MessageController
    participant Store as ProviderMessageStore
    participant Polling as PollingController
    participant UI as ui-whatsapp-simulator
    actor Paciente

    Backend->>Controller: POST mensagem ativa
    Controller->>Store: armazenar mensagem de saída
    Controller-->>Backend: referência da mensagem
    UI->>Polling: GET mensagens
    Polling->>Store: buscar mensagens ainda não consumidas
    Store-->>Polling: mensagens novas
    Polling-->>UI: mensagens novas
    UI-->>Paciente: exibe mensagem
```

## Polling do simulador web

```mermaid
sequenceDiagram
    participant UI as ui-whatsapp-simulator
    participant Polling as PollingController
    participant Store as ProviderMessageStore

    loop A cada 2 segundos
        UI->>Polling: GET mensagens após último cursor
        Polling->>Store: buscar mensagens novas
        Store-->>Polling: lista e próximo cursor
        Polling-->>UI: 200 OK com mensagens
    end
```
