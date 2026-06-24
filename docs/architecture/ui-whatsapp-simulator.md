# Frontend: ui-whatsapp-simulator

Repositório: `schambeck/ui-whatsapp-simulator`.

Este frontend simula a interface usada pelo paciente no WhatsApp. Ele conversa
somente com o `api-whatsapp-provider-simulator`; o webhook para o backend
principal é responsabilidade do provider.

## Componentes

```mermaid
flowchart TB
    subgraph UI["ui-whatsapp-simulator"]
        CHAT["ChatWindow"]
        INPUT["MessageInput"]
        LIST["MessageList"]
        POLLING["PollingService"]
        CLIENT["ProviderClient"]
    end

    PROVIDER["api-whatsapp-provider-simulator"]

    CHAT --> INPUT
    CHAT --> LIST
    INPUT --> CLIENT
    POLLING --> CLIENT
    POLLING --> LIST
    CLIENT -->|"HTTP POST / GET"| PROVIDER
```

## Fluxos de envio e recebimento

```mermaid
flowchart LR
    TYPE["Paciente digita"] --> INPUT["MessageInput valida"]
    INPUT --> POST["ProviderClient envia HTTP POST"]
    POST --> LOCAL["MessageList mostra mensagem enviada"]

    TIMER["Timer: 2 s"] --> POLL["PollingService executa HTTP GET"]
    POLL --> CHECK{"Há mensagens novas?"}
    CHECK -->|"sim"| APPEND["MessageList adiciona mensagens"]
    CHECK -->|"não"| TIMER
    APPEND --> TIMER
```

O polling deve evitar duplicação por identificador ou cursor e ser interrompido
quando a tela não estiver ativa.

## Sequência de polling

```mermaid
sequenceDiagram
    participant Chat as ChatWindow
    participant Polling as PollingService
    participant Client as ProviderClient
    participant Provider as api-whatsapp-provider-simulator
    participant List as MessageList

    Chat->>Polling: iniciar conversa
    loop A cada 2 segundos
        Polling->>Client: buscar mensagens desde cursor
        Client->>Provider: GET mensagens
        Provider-->>Client: mensagens e próximo cursor
        Client-->>Polling: resultado
        Polling->>List: anexar mensagens inéditas
    end
    Chat->>Polling: parar ao desmontar
```
