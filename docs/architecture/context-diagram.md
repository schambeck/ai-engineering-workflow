# Diagrama de contexto

O contexto abaixo mostra os usuários, os cinco projetos em repositórios
separados e uma integração municipal futura. O paciente pode usar o simulador
WhatsApp e, de forma complementar, o aplicativo mobile.

```mermaid
flowchart LR
    PATIENT["Paciente"]
    ADMIN_USER["Administrador UBS"]
    MUNICIPAL["Sistema Municipal / Saúde<br/>(futuro)"]

    subgraph SOLUTION["Solução Fila Virtual Transparente"]
        CHAT["ui-whatsapp-simulator<br/>schambeck/ui-whatsapp-simulator"]
        PROVIDER["api-whatsapp-provider-simulator<br/>schambeck/api-whatsapp-provider-simulator"]
        API["api-fila-virtual-transparente<br/>schambeck/api-fila-virtual-transparente"]
        ADMIN["ui-admin-fila-virtual<br/>schambeck/ui-admin-fila-virtual"]
        MOBILE["app-fila-virtual-mobile<br/>schambeck/app-fila-virtual-mobile"]
    end

    PATIENT -->|"conversa simulada"| CHAT
    PATIENT -->|"consulta e acompanha"| MOBILE
    ADMIN_USER -->|"opera a fila"| ADMIN
    CHAT -->|"HTTP"| PROVIDER
    PROVIDER -->|"webhook HTTP"| API
    API -->|"HTTP: mensagem ativa"| PROVIDER
    ADMIN -->|"HTTP"| API
    MOBILE -->|"HTTP"| API
    MUNICIPAL <-->|"API de integração<br/>(futuro)"| API
```

## Responsabilidades e chamadas

- O `ui-whatsapp-simulator` representa o canal do paciente e não acessa o
  backend principal diretamente.
- O `api-whatsapp-provider-simulator` recebe mensagens do simulador web,
  encaminha-as ao backend principal por webhook e disponibiliza mensagens de
  saída para polling.
- O `api-fila-virtual-transparente` concentra regras de negócio e persistência.
- O `ui-admin-fila-virtual` chama operações administrativas do backend por HTTP.
- O `app-fila-virtual-mobile` consulta e solicita operações do paciente por HTTP.
