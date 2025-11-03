# Organigrama del Proyecto Ruta K'ancha

Este documento muestra tres diagramas de flujo que ejemplifican la estructura organizacional híbrida descrita para el equipo Ruta K'ancha. Cada gráfico utiliza sintaxis Mermaid compatible con GitHub.

## Diagrama 1: Vista General del Organigrama

```mermaid
flowchart TD
    N0_Equipo["Equipo K'ancha<br/>Fundadores / Unidad de decisión estratégica<br/>Darío, Hector, Luis, Leydy"]
    N0_Equipo --> N1_Dario["Darío Quispe<br/>Team Lead · Project Manager · Lead Developer<br/>Convierte la visión en backlog ejecutable"]
    N1_Dario --> N2_Hector["Hector (...)<br/>Backend Developer<br/>Gestiona PostgreSQL y la API en Supabase"]
    N1_Dario --> N2_Luis["Luis Fernando Cutiri<br/>Frontend Developer (Android)<br/>Implementa la app nativa en Kotlin"]
    N1_Dario --> N2_Leydy["Leydy Rosalit Apaza<br/>UI·UX Designer · Data & Community Lead<br/>Lidera investigación, prototipos y feedback"]
```

## Diagrama 2: Cadena de Coordinación Operativa

```mermaid
flowchart TD
    N0_Equipo["Equipo K'ancha<br/>Define visión, hitos y pivotes estratégicos"] --> N1_Dario
    subgraph Cadena Operativa
        N1_Dario["Darío Quispe<br/>Dirige ceremonias Scrum y desbloquea impedimentos"] --> N2_Hector["Hector (...)<br/>Entrega servicios y datos confiables"]
        N1_Dario --> N2_Luis["Luis Fernando Cutiri<br/>Integra Material 3 y la API de rutas"]
        N1_Dario --> N2_Leydy["Leydy Rosalit Apaza<br/>Orquesta UX, recolección de datos y comunidad"]
    end
    N2_Hector --> N1_Dario
    N2_Luis --> N1_Dario
    N2_Leydy --> N1_Dario
```

## Diagrama 3: Flujo de Retroalimentación y Entregables

```mermaid
flowchart TD
    N0_Equipo["Equipo K'ancha<br/>Aprueba objetivos clave (Expotech, MVP)"] --> N1_Dario["Darío Quispe<br/>Traduce objetivos en tareas priorizadas"]
    N1_Dario --> N2_Hector["Hector (...)<br/>Implementa base de datos y API"]
    N1_Dario --> N2_Luis["Luis Fernando Cutiri<br/>Desarrolla la experiencia Android"]
    N1_Dario --> N2_Leydy["Leydy Rosalit Apaza<br/>Diseña flujos y lidera la comunidad"]

    N2_Hector --> entregables_backend["Entregable: API Supabase lista para consumo"]
    N2_Luis --> entregables_frontend["Entregable: App Kotlin alineada con Figma"]
    N2_Leydy --> entregables_diseno["Entregable: Investigación, prototipos y datos de rutas"]

    entregables_backend --> retro_equipo["Retroalimentación conjunta en dailies y reviews"]
    entregables_frontend --> retro_equipo
    entregables_diseno --> retro_equipo

    retro_equipo --> N0_Equipo["Fundadores evalúan progreso y ajustan estrategia"]
```
