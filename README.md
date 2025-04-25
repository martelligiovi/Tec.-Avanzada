# Diagrama de Clases

Este es el diagrama de clases del proyecto:

```mermaid
classDiagram
    class Espacio {
        -String id
        -String nombre
        -Double area
        -String ubicacion
        +Espacio(id, nombre, area, ubicacion)
        +getId() String
        +getNombre() String
        +getArea() Double
        +getUbicacion() String
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
        -boolean escenarioElevado
        -double precioUnico
        +getCapacidadAsientos() int
        +tieneEscenarioElevado() boolean
        +getPrecioUnico() double
        +setPrecioUnico(double precio) void
        +calcularPrecioEntrada() double
    }
    
    class Sala {
        -int capacidadPersonas
        -boolean sistemaAudiovisual
        -double precioEntradaTipoB
        +getCapacidadPersonas() int
        +tieneSistemaAudiovisual() boolean
        +getPrecioEntradaTipoB() double
        +setPrecioEntradaTipoB(double precio) void
        +calcularPrecioEntradaTipoA() double
        +calcularPrecioEntrada(String tipo) double
    }
    
    class Artista {
        -String id
        -String nombre
        -String genero
        -int popularidad
        +Artista(id, nombre, genero, popularidad)
        +getId() String
        +getNombre() String
        +getGenero() String
        +getPopularidad() int
        +calcularCacheMinimo() double
    }
    
    class Evento {
        -String id
        -String nombre
        -Date fecha
        -Time horaInicio
        -Time duracion
        -double precioBase
        -int entradasDisponibles
        +Evento(id, nombre, fecha, horaInicio, duracion, precioBase)
        +getId() String
        +getNombre() String
        +getFecha() Date
        +getHoraInicio() Time
        +getDuracion() Time
        +getPrecioBase() double
        +getEntradasDisponibles() int
        +reservarEntrada() boolean
        +calcularIngresosEstimados() double
        +esRentable() boolean
    }
    
    class Usuario {
        -String id
        -String nombre
        -String email
        -String telefono
        +Usuario(id, nombre, email, telefono)
        +getId() String
        +getNombre() String
        +getEmail() String
        +getTelefono() String
        +actualizarDatos(nombre, email, telefono) void
    }
    
    class Entrada {
        -String id
        -Date fechaCompra
        -double precio
        -String tipoEntrada
        -boolean utilizada
        +Entrada(id, evento, usuario, fechaCompra, precio, tipoEntrada)
        +getId() String
        +getFechaCompra() Date
        +getPrecio() double
        +getTipoEntrada() String
        +isUtilizada() boolean
        +marcarComoUtilizada() void
        +generarCodigoQR() String
    }
    
    Espacio "1" -- "1" Rol : tiene
    Rol <|-- Anfiteatro : es un
    Rol <|-- Sala : es un
    Evento "0..*" -- "1" Espacio : se realiza en
    Evento "0..*" -- "1..*" Artista : presenta a
    Usuario "1" -- "0..*" Entrada : compra
    Entrada "0..*" -- "1" Evento : pertenece a
