### Diagrama de Clases (Sistema de Gestión de Biblioteca)
```mermaid
classDiagram
    class RolUsuario {
        <<enumeration>>
        DOCENTE
        ALUMNO
        ADMIN
        BIBLIOTECARIO
    }

    class EstadoUsuario {
        <<enumeration>>
        ACTIVO
        INACTIVO
    }

    class EstadoReserva {
        <<enumeration>>
        PENDIENTE
        CERRADA
    }

    class EstadoEjemplar {
        <<enumeration>>
        PRESTADO
        DISPONIBLE
        BAJA
    }

    class Usuario {
        -id_PK
        -nombre
        -email
        -hashContraseña
        -cuil
        -EstadoUsuario estado
        -RolUsuario rol

        +GetId()
        +GetNombre()
        +GetEmail()
        +GethashContraseña()
        +GetCuil()
        +GetEstado()
        
        +SetNombre(nombre)
        +SetEmail(email)
        +SethashContraseña(contraseña)
        +SetCuil(cuil)
        +SetEstado(estado)

        +New(nombre, email, contraseña, cuil, estado)
        +Registrar()
        +IniciarSesion()
        +DarDeBaja()
        +ActivarUsuario()
    }

    class Libro {
        -id_PK
        -titulo
        -autor
        +New(id, titulo, autor)
        +GetId()
        +GetTitulo()
        +GetAutor()
        +BuscarLibro(titulo)
    }

    class Ejemplar {
        -ISBN_PK
        -LibroId_FK
        -Ubicación
        -EstadoEjemplar estado

        +New(ISBN, LibroId, Ubicación, Disponibilidad)
        +GetISBN()
        +GetLibroId()
        +GetUbicación()
        +GetDisponibilidad()
        +GetDisponibles()
        +SetUbicación(ubicación)
        +SetEstado(estado)
    }

    class Prestamo {
        -id_PK
        -EjemplarId_FK
        -UsuarioId_FK
        -fechaInicial
        -fechaVencimiento
        -fechaDevolución

        +New(EjemplarId, UsuarioId, fechaInicial)
        +Getid()
        +GetEjemplarId()
        +GetUsuarioId()
        +GetfechaInicial()
        +GetfechaVencimiento()
        +GetfechaDevolución()
        +SetFechaVencimiento(fecha)
        +SetfechaDevolución(fecha)
        +CalcularMulta()
        +TerminarPrestamo()
    }

    class Reserva {
        - Id_PK
        - clienteId_FK
        - libroId_FK
        - fecha
        - EstadoReserva estado


        + new (Id, usuarioId , libroId )
        + GetId()
        + GetUsuarioId()
        + GetlibroId()
        + GetFecha()
        + GetReservasPendientes()
        + GetReservaPorId(reservaId)

        + SetEstado(estado)
    }

    Libro "1" -- "0..*" Ejemplar
    Prestamo "*" -- "1" Ejemplar
    Prestamo "*" -- "1" Usuario
    Reserva "*" -- "1" Libro
    Reserva "*" -- "1" Usuario
    RolUsuario -- Usuario
    EstadoUsuario -- Usuario    
    EstadoReserva -- Reserva    
    EstadoEjemplar -- Ejemplar    

```