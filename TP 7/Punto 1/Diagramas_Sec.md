### A. Ingreso de un nuevo cliente (SEC-01)

```mermaid
sequenceDiagram
    actor Cliente
    Cliente->>+cliente: ingreso()
    cliente-->>+Cliente: ingreso()

```

-----------------------

### B. Registro de un cliente (SEC-02)

```mermaid
sequenceDiagram
    actor Cliente
    
    Cliente->>+cliente: new(Nombre, Teléfono,  E-mail,  CUIL)
    cliente-->>+Cliente: return Ok || Error
    Note left of Cliente: El estado "activo" implica <br> que el usuario este registrado
    Cliente->>+cliente: activarUsuario()
    cliente-->>+Cliente: return Ok || Error
```

-----------------------

### C. Acceso de un cliente (SEC-03)

```mermaid
sequenceDiagram
    actor Cliente

    Cliente->>+cliente: loginCliente()
    cliente-->>+Cliente: return Ok || Error
    Note left of Cliente: Se requiere que el cliente <br> este previamente registrado (activo)
```

-----------------------
### D. Cambio de Password (SEC-04)
```mermaid
sequenceDiagram
    actor Cliente

    Cliente->>+cliente: loginCliente()
    cliente-->>+Cliente: return Ok || Error
    
    Cliente->>+cliente: cambiarContraseña()
    cliente-->>+Cliente: return Ok || Error
    
    
    Note left of Cliente: Se requiere que el cliente <br> este previamente registrado (activo)
```

-----------------------

### E. Actualizacion de datos de un cliente (SEC-05)
```mermaid
sequenceDiagram
    actor Cliente

    Cliente->>+cliente: loginCliente()
    cliente-->>+Cliente: return Ok || Error

    Cliente->>+cliente: actualizarDatos()
    Note right of cliente: Se actualizan los atributos: <br> Nombre, Teléfono, E-mail, CUIL 
    cliente-->>+Cliente: return Ok || Error
```

-----------------------

### F. Abrir nuevo ticket (SEC-06)
```mermaid
sequenceDiagram
    actor Cliente

    participant cliente
    participant Ticket 
    participant Log


    Cliente->>+cliente: loginCliente()
    cliente-->>+Cliente: return Ok || Error

    Cliente->>+Ticket: new(Cliente.Id, Descripcion, TipoDeRespuesta)

    Ticket->>+Log: new(Ticket.ID, FechaCreacion, Descripción)

    Log-->>+Ticket: return Ok || Error
    
    Ticket-->>+Cliente: return Ok || Error
```

-----------------------

### G. Actualizar ticket (SEC-07)
```mermaid
sequenceDiagram
    actor Cliente
    
    participant cliente 
    participant Ticket
    participant Log

    Cliente->>+cliente: logIn(E-mail, Contraseña)
    cliente-->>+Cliente: return Ok || Error

    Cliente->>+Ticket: getTicket(Ticket.ID)
    Ticket-->>+Cliente: return (descripcion, estado, fechaCreacion, fechaCierre, <br>FechaUltimaActualizacion) || Error

    Cliente->>+Ticket: cambiarDescripcion()
    Ticket->>Log: new(Ticket.ID, FechaCreacion, Descripción)
    Log->>Ticket: return Ok || Error

    Ticket->>Cliente: return Ok || Error
    
```

-----------------------
### H. Consultar tickets existentes (SEC-08)

```mermaid
sequenceDiagram
    Note right of cliente: Se actualizan los atributos: <br> Nombre, Teléfono, E-mail, CUIL 

    actor cliente
    participant Cliente
    participant Ticket

    Cliente->>+cliente: loginCliente()
    cliente-->>+Cliente: return Ok || Error

    Cliente->>+Ticket: listarTickets()    
    Ticket-->>+Cliente: return (descripcion, estado, fechaCreacion, <br>fechaCierre, <br>FechaUltimaActualizacion) || Error
```
-----------------------

### I. Borrar ticket (SEC-09)
```mermaid  
sequenceDiagram
    actor Cliente
    
    participant cliente 
    participant Ticket
    participant Log

    Note left of Cliente: Se requiere que el cliente este <br>previamente registrado (activo)
    Cliente->>+cliente: loginCliente()
    cliente-->>+Cliente: return Ok || Error

    Cliente->>+Ticket: getTicket(Ticket.ID)
    Ticket-->>+Cliente: return (descripcion, estado, fechaCreacion, fechaCierre, <br>FechaUltimaActualizacion) || Error

    Cliente->>+Ticket: cambiarDescripcion()
    Note left of Cliente: Cerrar ticket implica considerarlo como<br> inactivo internamente, aunque sin eliminar<br> la entidad del sistema
    Ticket->>Log: new(Ticket.ID, FechaCreacion, Descripción)
    Log->>Ticket: return Ok || Error
    Ticket->>Cliente: return Ok || Error
    
```
-----------------------
