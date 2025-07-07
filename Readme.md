# Ampliación de Contenidos Audiovisuales

Este proyecto es una ampliación de un sistema de gestión de contenidos audiovisuales desarrollado en Java, utilizando conceptos de Programación Orientada a Objetos (POO) como herencia, asociación y agregación. El objetivo es modelar diferentes tipos de contenidos audiovisuales y sus relaciones con otros elementos.

## Estructura del Proyecto

El proyecto está organizado en paquetes:

* **`uni1a`**: Contiene las clases principales del modelo de datos de los contenidos audiovisuales y sus entidades relacionadas.
    * `ContenidoAudiovisual` (Clase abstracta base)
    * `Pelicula`
    * `SerieDeTV`
    * `Documental`
    * `Concierto` (Nueva en Etapa 4)
    * `Podcast` (Nueva en Etapa 4)
    * `Actor` (Entidad relacionada con Película)
    * `Temporada` (Entidad relacionada con SerieDeTV)
    * `Investigador` (Entidad relacionada con Documental)
* **`poo`**: Contiene la clase principal para la ejecución y prueba del sistema.
    * `PruebaAudioVisual`

## Clases y Relaciones

### Clases Base y Heredadas:

* **`ContenidoAudiovisual` (Abstracta)**: Clase padre que define los atributos y comportamientos comunes para todos los tipos de contenido (título, duración, género, ID).
* **`Pelicula`**: Hereda de `ContenidoAudiovisual`. Atributo adicional: `estudio`. Se asocia con `Actor`.
* **`SerieDeTV`**: Hereda de `ContenidoAudiovisual`. Atributo adicional: `temporadas`. Agrega objetos `Temporada`.
* **`Documental`**: Hereda de `ContenidoAudiovisual`. Atributo adicional: `tema`. Se asocia con `Investigador`.
* **`Concierto`**: (NUEVA) Hereda de `ContenidoAudiovisual`. Atributos adicionales: `artistaPrincipal`, `lugar`. Agrega una lista de `cancionesInterpretadas`.
* **`Podcast`**: (NUEVA) Hereda de `ContenidoAudiovisual`. Atributos adicionales: `host`, `numeroEpisodiosTotales`. Agrega una lista de `temasPrincipales`.

### Clases de Apoyo (Relacionadas):

* **`Actor`**: Representa a un actor con `nombre` y `nacionalidad`. (Asociación con `Pelicula`)
* **`Temporada`**: Representa una temporada de una serie con `numeroTemporada`, `numeroEpisodios` y una lista de `titulosEpisodios`. (Agregación con `SerieDeTV`)
* **`Investigador`**: Representa a un investigador con `nombre` y `especialidad`. (Asociación con `Documental`)

## Diagrama de Clases (PlantUML)

```plantuml
@startuml
!theme plain

abstract class ContenidoAudiovisual {
    -static int contar
    -String titulo
    -int duracionEnMinutos
    -String genero
    -int id
    +ContenidoAudiovisual(titulo: String, duracionEnMinutos: int, genero: String)
    +getTitulo(): String
    +setTitulo(titulo: String): void
    +getDuracionEnMinutos(): int
    +setDuracionEnMinutos(duracionEnMinutos: int): void
    +getGenero(): String
    +setGenero(genero: String): void
    +getId(): int
    +abstract mostrarDetalles(): void
}

class Pelicula extends ContenidoAudiovisual {
    -String estudio
    +Pelicula(titulo: String, duracionEnMinutos: int, genero: String, estudio: String)
    +getEstudio(): String
    +setEstudio(estudio: String): void
    +agregarActor(actor: Actor): void
    +mostrarDetalles(): void
}

class SerieDeTV extends ContenidoAudiovisual {
    -int temporadas
    +SerieDeTV(titulo: String, duracionEnMinutos: int, genero: String, temporadas: int)
    +getTemporadas(): int
    +setTemporadas(temporadas: int): void
    +agregarTemporada(temporada: Temporada): void
    +mostrarDetalles(): void
}

class Documental extends ContenidoAudiovisual {
    -String tema
    +Documental(titulo: String, duracionEnMinutos: int, genero: String, tema: String)
    +getTema(): String
    +setTema(tema: String): void
    +agregarInvestigador(investigador: Investigador): void
    +mostrarDetalles(): void
}

class Concierto extends ContenidoAudiovisual {
    -String artistaPrincipal
    -String lugar
    -List<String> cancionesInterpretadas
    +Concierto(titulo: String, duracionEnMinutos: int, genero: String, artistaPrincipal: String, lugar: String)
    +getArtistaPrincipal(): String
    +setArtistaPrincipal(artistaPrincipal: String): void
    +getLugar(): String
    +setLugar(lugar: String): void
    +agregarCancion(cancion: String): void
    +getCancionesInterpretadas(): List<String>
    +mostrarDetalles(): void
}

class Podcast extends ContenidoAudiovisual {
    -String host
    -int numeroEpisodiosTotales
    -List<String> temasPrincipales
    +Podcast(titulo: String, duracionEnMinutos: int, genero: String, host: String, numeroEpisodiosTotales: int)
    +getHost(): String
    +setHost(host: String): void
    +getNumeroEpisodiosTotales(): int
    +setNumeroEpisodiosTotales(numeroEpisodiosTotales: int): void
    +agregarTema(tema: String): void
    +getTemasPrincipales(): List<String>
    +mostrarDetalles(): void
}

class Actor {
    -String nombre
    -String nacionalidad
    +Actor(nombre: String, nacionalidad: String)
    +getNombre(): String
    +setNombre(nombre: String): void
    +getNacionalidad(): String
    +setNacionalidad(nacionalidad: String): void
    +mostrarDetalles(): void
}

class Temporada {
    -int numeroTemporada
    -int numeroEpisodios
    -List<String> titulosEpisodios
    +Temporada(numeroTemporada: int, numeroEpisodios: int)
    +getNumeroTemporada(): int
    +setNumeroTemporada(numeroTemporada: int): void
    +getNumeroEpisodios(): int
    +setNumeroEpisodios(numeroEpisodios: int): void
    +agregarEpisodio(tituloEpisodio: String): void
    +getTitulosEpisodios(): List<String>
    +mostrarDetalles(): void
}

class Investigador {
    -String nombre
    -String especialidad
    +Investigador(nombre: String, especialidad: String)
    +getNombre(): String
    +setNombre(nombre: String): void
    +getEspecialidad(): String
    +setEspecialidad(especialidad: String): void
    +mostrarDetalles(): void
}

' Relaciones de Herencia
ContenidoAudiovisual <|-- Pelicula
ContenidoAudiovisual <|-- SerieDeTV
ContenidoAudiovisual <|-- Documental
ContenidoAudiovisual <|-- Concierto
ContenidoAudiovisual <|-- Podcast

' Relaciones de Asociación/Agregación
Pelicula "1" -- "*" Actor : tiene >
SerieDeTV "1" o-- "*" Temporada : contiene >
Documental "1" -- "*" Investigador : involucra >
Concierto "1" o-- "*" CancionesInterpretadas : interpreta >

@enduml