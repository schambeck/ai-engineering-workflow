# Diagrama de containers

Os containers são distribuídos entre cinco repositórios de aplicação. O
PostgreSQL é acessado exclusivamente pelo backend principal.

```mermaid
flowchart TB
    PATIENT["Paciente"]
    ADMIN_USER["Administrador UBS"]

    subgraph FRONTENDS["Frontends"]
        CHAT["React Web<br/>ui-whatsapp-simulator"]
        ADMIN["React Web<br/>ui-admin-fila-virtual"]
        MOBILE["App mobile<br/>app-fila-virtual-mobile"]
    end

    subgraph BACKENDS["Backends"]
        PROVIDER["Spring Boot API<br/>api-whatsapp-provider-simulator"]
        API["Spring Boot API<br/>api-fila-virtual-transparente"]
    end

    DB[("PostgreSQL<br/>dados da fila")]

    PATIENT --> CHAT
    PATIENT --> MOBILE
    ADMIN_USER --> ADMIN

    CHAT -->|"HTTP POST: enviar mensagem"| PROVIDER
    CHAT -->|"HTTP GET: polling a cada 2 s"| PROVIDER
    PROVIDER -->|"webhook HTTP: mensagem recebida"| API
    API -->|"HTTP: mensagem ativa"| PROVIDER
    ADMIN -->|"HTTP: consultar/operar fila"| API
    MOBILE -->|"HTTP: status e solicitações"| API
    API -->|"SQL / transações"| DB
```

## Protocolos

| Origem | Destino | Comunicação |
| --- | --- | --- |
| `ui-whatsapp-simulator` | `api-whatsapp-provider-simulator` | HTTP POST para envio e HTTP GET por polling a cada 2 segundos. |
| `api-whatsapp-provider-simulator` | `api-fila-virtual-transparente` | Webhook HTTP para mensagens recebidas. |
| `api-fila-virtual-transparente` | `api-whatsapp-provider-simulator` | HTTP para mensagens ativas e respostas ao paciente. |
| `ui-admin-fila-virtual` | `api-fila-virtual-transparente` | HTTP para dashboard e comandos administrativos. |
| `app-fila-virtual-mobile` | `api-fila-virtual-transparente` | HTTP para identificação, fila, reservas e histórico. |
| `api-fila-virtual-transparente` | PostgreSQL | Acesso transacional aos dados da solução. |
