# Pokédex — Frontend

Prototipo funcional de la interfaz de la Pokédex: catálogo de Pokémon, equipos, favoritos y
estadísticas, consumiendo la [Pokédex API](#) <!-- reemplazar con el link al repo de backend -->.

> 🎨 **Prototipo en Figma:** [enlace al prototipo](#) <!-- reemplazar con el link real de Figma -->

## Tabla de contenidos

1. [Descripción del proyecto](#descripción-del-proyecto)
2. [Manual de identidad](#manual-de-identidad)
3. [Diagramas](#diagramas)

## Descripción del proyecto

<!-- Describir aquí en 1-2 párrafos: qué hace la interfaz, a quién va dirigida (Guest/Trainer/Admin),
     y qué flujos principales cubre el prototipo (ver catálogo, filtrar, armar equipos, marcar favoritos,
     ver estadísticas, panel de administración). -->

## Manual de identidad

<!-- Aquí va la guía de estilo visual del prototipo: paleta de colores, tipografía, logo,
     componentes reutilizables (botones, cards, inputs), tono de la marca. -->

### Paleta de colores

| Color | Hex | Uso |
|---|---|---|
| | | |

### Tipografía

<!-- Familia tipográfica principal y secundaria, tamaños de encabezados/cuerpo -->

### Componentes base

<!-- Botones, cards de Pokémon, badges de tipo, navegación, etc. -->

## Diagramas

### Diagrama de contexto (C4 — Nivel 1)

Muestra el sistema como caja negra, sus actores y la integración externa con Google.

```mermaid
---
config:
  theme: dark
  flowchart:
    curve: linear
    nodeSpacing: 40
    rankSpacing: 70
---
flowchart LR
    Guest["Guest<br/>Visitante sin cuenta"]
    Trainer["Trainer<br/>Entrenador registrado"]
    Admin["Admin<br/>Administrador del catálogo"]

    App["Pokédex<br/>Catálogo, equipos, favoritos y estadísticas de Pokémon"]

    Google["Google<br/>Proveedor de login OAuth2"]

    Guest -->|"consulta el catálogo"| App
    Trainer -->|"gestiona equipos y favoritos"| App
    Admin -->|"administra el catálogo"| App
    App -->|"autentica con"| Google

    classDef actor fill:#1b2d4f,stroke:#5a8bf0,color:#ffffff
    classDef system fill:#1a3f1f,stroke:#5fe080,color:#ffffff
    classDef ext fill:#101010,stroke:#ffffff,color:#ffffff

    class Guest,Trainer,Admin actor
    class App system
    class Google ext
```

### Diagrama de componentes general (C4 — Nivel 2)

Muestra las piezas internas del sistema: Frontend, Backend (API monolítica por capas) y las
bases de datos.

```mermaid
---
config:
  theme: dark
  flowchart:
    curve: linear
    nodeSpacing: 40
    rankSpacing: 70
---
flowchart LR
    Guest["Guest"]
    Trainer["Trainer"]
    Admin["Admin"]

    Front["Frontend Web/Mobile<br/>Prototipo Figma / SPA"]
    Back["Pokédex API<br/>Spring Boot · Controller, Core, Persistence, Security, Config"]
    PG[("PostgreSQL<br/>Catálogo, usuarios, equipos, favoritos")]
    Mongo[("MongoDB<br/>Estadísticas de vistas y elecciones")]

    Google["Google<br/>OAuth2"]

    Guest --> Front
    Trainer --> Front
    Admin --> Front
    Front -->|"REST / JSON + JWT"| Back
    Back --> PG
    Back --> Mongo
    Back -->|"autentica con"| Google

    classDef actor fill:#1b2d4f,stroke:#5a8bf0,color:#ffffff
    classDef frontend fill:#2c2c2a,stroke:#888780,color:#ffffff
    classDef backend fill:#1a3f1f,stroke:#5fe080,color:#ffffff
    classDef db fill:#0f1a0f,stroke:#5fe080,color:#ffffff
    classDef ext fill:#101010,stroke:#ffffff,color:#ffffff

    class Guest,Trainer,Admin actor
    class Front frontend
    class Back backend
    class PG,Mongo db
    class Google ext
```
