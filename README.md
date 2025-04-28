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
        -String tipo
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

```
----------
## Modelo de Datos

No se realiza un modelo de datos manual ya que se utilizará un **ORM (Entity Framework)** para la gestión de la base de datos.

----------
## Tecnologías Utilizadas

- **.NET 8**
- **Aplicación Web Blazor**
- **SQL Server**
- **Entity Framework** (ORM)
- **xUnit** (para testing unitario)


----------
## Alcance del Testeo Unitario

### Cobertura Funcional
- Se testearán únicamente los **métodos públicos** de cada clase, ignorando implementaciones internas.

### Casos de Prueba Cubiertos (Caja Negra)
- Validaciones de **entradas válidas** e **inválidas**.
- Resultados esperados frente a diferentes combinaciones de **datos de entrada**.

### Exclusiones del Testeo
- Implementaciones internas no accesibles desde la API pública de las clases.
- Aspectos relacionados con:
  - La **interfaz de usuario (UI)**.
  - La **integración con bases de datos** (estos serán abordados mediante tests de integración en otros enfoques).

> 🔹 **Nota:** El alcance de este documento se limita exclusivamente a **tests unitarios**.

## Prioridades

- **Alta Prioridad**: Usuario, Entrada, Evento.
- **Media Prioridad**: Espacio, Rol, Sala.
----------
## Justificación de la Elección de Tecnología y Consideraciones

- Utilizaré **.NET 8** y una **Aplicación Web Blazor**, ya que en la empresa donde trabajo se utiliza este stack y deseo capacitarme en el mismo.

- Emplearé **Entity Framework** como ORM, dado que facilita la creación de aplicaciones al:
  - Simplificar la manipulación de datos.
  - Proporcionar una capa de seguridad adicional contra **inyecciones SQL**, ya que maneja internamente la mayoría de los patrones de inyección conocidos.

- Para las pruebas unitarias, usaré **xUnit**, ya que es la herramienta de testeo más popular en el ecosistema .NET.
  - Cuenta con una **gran comunidad** de soporte.
  - Es una herramienta **madura y bien testeada**, lo que garantiza confiabilidad y facilidad de aprendizaje.

