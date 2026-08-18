### Diagrama de Secuencia (Generar Reserva de un Libro)

```mermaid
sequenceDiagram

    actor Estudiante as Estudiante
    participant UserEst as User(Estudiante)
    participant Libro as Libro

    participant Reserva as Reserva


    Estudiante ->> UserEst: login()
    UserEst -->> Estudiante: return Ok || Error

    Estudiante ->> Libro: buscarLibro()
    Libro -->> Estudiante: return idLibro || Error

    Estudiante ->> Reserva: new( usuarioId, libroId)
    Reserva -->> Estudiante: return Ok || Error
    


    
    %% camino de error
    
```
---
### Diagrama de Secuencia (Cerrar Reserva y Registrar préstamo de un libro)
```mermaid
sequenceDiagram


    actor Bibliotecario as Bibliotecario
    participant UserBiblo as User(Bibliotecario)
    participant Ejemplar as Ejemplar
    participant Prestamo as Prestamo
    participant Reserva as Reserva



    Bibliotecario ->> UserBiblo: login()
    UserBiblo -->> Bibliotecario: return Ok || Error
    

    Bibliotecario ->> Reserva: GetReservasPendientes()
    Reserva -->> Bibliotecario: return reservaID || Error

    Bibliotecario ->> Ejemplar: GetDisponibles()
    Ejemplar -->> Bibliotecario: return ejemplarId || Error

    Bibliotecario ->> Prestamo: new (EjemplarId, UsuarioId, fechaInicial)

    Prestamo -->> Bibliotecario: return Ok || Error

    Bibliotecario ->> Reserva: SetEstado(estado)
    Reserva -->> Bibliotecario: return Ok || Error
    
```
---
### Diagrama de Secuencia (Terminar prestamo y Pago de multa)
```mermaid
sequenceDiagram
    actor Usuario Lector
    participant Usuario
    participant Prestamo

    Usuario Lector->>Usuario: login()
    Usuario-->>Usuario Lector: Ok | Err

    Usuario->>Prestamo: BuscarPrestamo()
    Prestamo-->>Usuario: prestamoID | Err

    Usuario->>Prestamo: terminarPrestamo(prestamoID)
    
    alt Tiene multa
        Prestamo-->>Usuario: return CalcularMulta()

        Usuario->>Prestamo: PagarMulta()

        Prestamo-->>Usuario: Ok | Err
    else No tiene multa
        Prestamo-->>Usuario: Ok | Err
    end
```