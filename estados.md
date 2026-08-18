```mermaid

stateDiagram-v2

    [*] --> Disponible : New()
    Disponible --> Prestado : setEstado(prestado)
    Disponible --> Baja : setEstado(baja)
    Prestado --> Baja : setEstado(baja)


```