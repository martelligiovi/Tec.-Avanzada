# Diagrama de Clases

Este es el diagrama de clases del proyecto:

```mermaid
classDiagram
    %% Enumeración para los tipos de entrada
    class TipoEntrada {
        <<enumeration>>
        A
        B
        GENERAL
    }

    %% Clases principales
    class Espacio {
        -String id
        -String nombre
        +Espacio(id, nombre)
        +getId() String
        +getNombre() String
        +calcularCapacidad() int
    }

    class Rol {
        -String id
        -String nombre
        -String descripcion
        +Rol(id, nombre, descripcion)
        +getId() String
        +getNombre() String
        +getDescripcion() String
        +calcularPrecioEntrada() double
    }

    class Anfiteatro {
        -int capacidadAsientos
        +Anfiteatro(capacidadAsientos)
        +getCapacidadAsientos() int
    }

    class Sala {
        -Map~TipoAsiento,Integer~ capacidades
        +Sala(capA, capB)
        +getCapacidad(TipoEntrada) int
        +calcularPrecioEntrada(TipoAsiento, double) double
    }

    class Artista {
        -String id
        -String nombre
        +Artista(id, nombre)
        +getId() String
        +getNombre() String
    }

    class Evento {
        -String id
        -String nombre
        -Date fecha
        -Time horaInicio
        -Time horaFin
        -double precioBase 
        -int entradasDisponibles
        +Evento(id, nombre, fecha, horaInicio, horaFin, precioBase)
        +getId() String
        +getNombre() String
        +getFecha() Date
        +getHoraInicio() Time
        +getHoraFin() Time
        +getPrecioBase() double
        +getEntradasDisponibles() int
        +getEntradasVendidas(TipoEntrada) int
        +registrarVenta(TipoEntrada) void
        +calcularIngresos() double
        +getPrecioEntradas() Map~TipoAsiento,Integer~
    }

    class Usuario {
        -String id
        -String email
        -String password
        +Usuario(id,email, password)
        +getId() String
        +getEmail() String
        +login(email, password) boolean
    }

    class Entrada {
        -String id
        -Date fechaCompra
        -double precio
        -TipoEntrada tipo
        -boolean utilizada
        +Entrada(id, evento, usuario, fechaCompra, TipoEntrada)
        +getId() String
        +getFechaCompra() Date
        +getPrecio() double
        +getTipo() TipoEntrada
        +isUtilizada() boolean
        +marcarComoUtilizada() void
        +generarCodigoQR() String
    }

    %% Relaciones
    Espacio "0" -- "1" Rol : tiene
    Rol <|-- Anfiteatro : es un
    Rol <|-- Sala : es un
    Evento "0..*" -- "1" Espacio : se realiza en
    Evento "0..*" -- "1..*" Artista : presenta a
    Usuario "1" -- "0..*" Entrada : Tiene una
    Entrada "0..*" -- "1" Evento : pertenece a
