# Modelo de dados conceitual

O modelo abaixo é conceitual e pertence ao domínio do
`api-fila-virtual-transparente`. Tabelas, colunas, cardinalidades opcionais e
tipos devem ser confirmados no repositório da API e em suas migrações.

```mermaid
erDiagram
    Patient ||--o{ Conversation : inicia
    Patient ||--o{ QueueEntry : possui
    Patient ||--o{ Reservation : solicita
    Conversation ||--o{ MessageLog : registra
    Conversation o|--o| QueueEntry : origina
    Reservation }o--|| Slot : ocupa
    QueueEntry o|--o| Reservation : pode_gerar

    Patient {
        uuid id
        string cpf
        string cns
        string name
    }

    Conversation {
        uuid id
        uuid patient_id
        string channel
        string state
    }

    QueueEntry {
        uuid id
        uuid patient_id
        string state
        int priority
        datetime enqueued_at
    }

    Reservation {
        uuid id
        uuid patient_id
        uuid slot_id
        string status
    }

    Slot {
        uuid id
        datetime starts_at
        string service_type
        string status
    }

    MessageLog {
        uuid id
        uuid conversation_id
        string direction
        string delivery_status
        datetime created_at
    }
```

## Limites do modelo

```mermaid
flowchart LR
    PROVIDER["Provider WhatsApp"] -->|"eventos e referências"| MESSAGE["MessageLog"]
    DOMAIN["Serviços de domínio"] --> PATIENT["Patient"]
    DOMAIN --> CONVERSATION["Conversation"]
    DOMAIN --> QUEUE["QueueEntry"]
    DOMAIN --> RESERVATION["Reservation / Slot"]
    PATIENT --> DB[("PostgreSQL")]
    CONVERSATION --> DB
    QUEUE --> DB
    RESERVATION --> DB
    MESSAGE --> DB
```

- `QueueEntry.state` segue `WAITING`, `CALLED`, `IN_SERVICE`, `COMPLETED`,
  `CANCELLED` e `EXPIRED`.
- Estados de `Conversation`, reservas e slots são propostos e ainda precisam de
  contrato de domínio.
- Restrições de unicidade para CPF/CNS e uma entrada ativa por fila devem ser
  definidas ou confirmadas nas migrações.
