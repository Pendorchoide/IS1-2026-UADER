
```mermaid
---
title: Diagrama de Paquetes
---
flowchart TB

    subgraph GestionClientes [Gestión de Clientes]
        Cliente[Cliente]
    end

    subgraph GestionTickets [Gestión de Tickets]
        Ticket[Ticket]
        AnalistaTicket[AnalistaTicket]
        Analista[Analista]
        Log[Log]
    end

    Cliente --- Ticket
    Ticket --- Log
    Ticket --- AnalistaTicket
    AnalistaTicket --- Analista

    GestionClientes -.->|<< access >>| GestionTickets

```