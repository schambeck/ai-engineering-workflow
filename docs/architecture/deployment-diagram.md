# Diagramas de deployment

Os diagramas separam a topologia local de desenvolvimento da topologia futura.
Portas, provedores de nuvem e ferramentas de empacotamento devem ser definidos
nos repositórios de aplicação.

## Local / desenvolvimento

```mermaid
flowchart TB
    subgraph MACHINE["Máquina do desenvolvedor ou Docker Compose"]
        BROWSER["Navegador"]
        DEVICE["Emulador / dispositivo mobile"]
        CHAT["React<br/>ui-whatsapp-simulator"]
        ADMIN["React<br/>ui-admin-fila-virtual"]
        MOBILE["app-fila-virtual-mobile"]
        PROVIDER["Spring Boot<br/>api-whatsapp-provider-simulator"]
        API["Spring Boot<br/>api-fila-virtual-transparente"]
        DB[("PostgreSQL")]

        BROWSER --> CHAT
        BROWSER --> ADMIN
        DEVICE --> MOBILE
        CHAT -->|"HTTP + polling"| PROVIDER
        PROVIDER -->|"webhook HTTP"| API
        API -->|"HTTP"| PROVIDER
        ADMIN -->|"HTTP"| API
        MOBILE -->|"HTTP"| API
        API -->|"SQL"| DB
    end
```

## Futuro: cloud ou ambiente municipal/on-premise

```mermaid
flowchart TB
    USERS["Pacientes e administradores"]

    subgraph ENV["Cloud ou datacenter municipal / on-premise (futuro)"]
        PROXY["Nginx / reverse proxy<br/>TLS e roteamento"]

        subgraph WEB["Hospedagem de frontends"]
            CHAT["React<br/>ui-whatsapp-simulator<br/>(somente homologação)"]
            ADMIN["React<br/>ui-admin-fila-virtual"]
        end

        subgraph APPS["Runtime de aplicações"]
            PROVIDER["Spring Boot<br/>api-whatsapp-provider-simulator<br/>(homologação)"]
            API["Spring Boot<br/>api-fila-virtual-transparente"]
        end

        DB[("PostgreSQL gerenciado<br/>ou institucional")]
        MON["Logs, métricas e auditoria<br/>(futuro)"]
    end

    MOBILE["app-fila-virtual-mobile"]
    MUNICIPAL["Sistema Municipal / Saúde<br/>(futuro)"]

    USERS --> PROXY
    USERS --> MOBILE
    PROXY --> CHAT
    PROXY --> ADMIN
    PROXY --> PROVIDER
    PROXY --> API
    CHAT -->|"polling"| PROVIDER
    PROVIDER -->|"webhook"| API
    ADMIN -->|"HTTP"| API
    MOBILE -->|"HTTPS"| API
    MUNICIPAL <-->|"HTTPS / integração futura"| API
    API --> DB
    API -.-> MON
    PROVIDER -.-> MON
```

Em produção, o simulador pode ser substituído por um provider WhatsApp real. O
reverse proxy, alta disponibilidade, gestão de segredos, backup e observabilidade
são elementos futuros.
