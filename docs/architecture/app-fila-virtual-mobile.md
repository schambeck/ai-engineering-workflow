# Aplicativo: app-fila-virtual-mobile

Repositório: `schambeck/app-fila-virtual-mobile`.

O aplicativo oferece um canal complementar ao WhatsApp para o paciente. Telas,
rotas e contratos exatos são **propostos** até validação no repositório do app.

## Fluxo de navegação

```mermaid
flowchart TD
    START([Início]) --> ID["Identificação<br/>CPF ou CNS"]
    ID --> HOME["Home"]
    HOME --> STATUS["Status da fila"]
    HOME --> OPTIONS["Opções de atendimento"]
    OPTIONS --> CONFIRM["Confirmação"]
    CONFIRM --> STATUS
    HOME --> HISTORY["Histórico"]
    STATUS --> HOME
    HISTORY --> HOME
```

## Consulta da posição na fila

```mermaid
sequenceDiagram
    actor Paciente
    participant App as app-fila-virtual-mobile
    participant API as api-fila-virtual-transparente
    participant DB as PostgreSQL

    Paciente->>App: Abre "Status da fila"
    App->>API: GET posição do paciente
    API->>DB: consultar QueueEntry ativa e ordenação
    DB-->>API: estado e dados necessários à posição
    API-->>App: posição, estado e última atualização
    App-->>Paciente: exibe status da fila
```

## Relação entre telas e backend

```mermaid
flowchart LR
    ID["CPF/CNS"] -->|"HTTP: identificar"| API["api-fila-virtual-transparente"]
    STATUS["Status da fila"] -->|"HTTP: consultar posição"| API
    OPTIONS["Opções de atendimento"] -->|"HTTP: listar opções"| API
    CONFIRM["Confirmação"] -->|"HTTP: criar fila/reserva"| API
    HISTORY["Histórico"] -->|"HTTP: consultar atendimentos"| API
```

Dados de outros pacientes não devem ser expostos na consulta de posição.
