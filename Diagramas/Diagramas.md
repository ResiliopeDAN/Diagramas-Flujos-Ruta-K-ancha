# Diagramas de Flujo - Ruta K'ancha

Este documento presenta los diagramas de flujo para los tres flujos principales del prototipo de la aplicación Ruta K'ancha. Cada diagrama está definido utilizando la sintaxis Mermaid (flowchart TD).

## Flujo 1: Onboarding (Carrusel de Bienvenida)

```mermaid
flowchart TD
    A(Inicio: Usuario abre la app por 1ra vez) --> B[Pantalla: Bienvenida (Slide 1)\n"Bienvenido a Ruta K'ancha"];
    B --> C(Acción: Usuario desliza);
    C --> D[Pantalla: Valor 1 (Slide 2)\n"Encuentra tu ruta más rápida"];
    D --> E(Acción: Usuario desliza);
    E --> F[Pantalla: Valor 2 (Slide 3)\n"Ahorra tiempo y dinero"];
    F --> G(Acción: Toca "Comenzar");
    G --> H[Pop-up: Solicitud de Permiso de Ubicación\n"Ruta K'ancha necesita tu ubicación..."];

    H --> I{Acción: Usuario elige permiso};
    I -- "Permitir (Recomendado)" --> J[Estado del Sistema: GPS Activado];
    I -- "Solo esta vez" --> J;
    I -- "Rechazar" --> K[Estado del Sistema: GPS Desactivado];

    J --> L(Fin: Ir a Pantalla Principal);
    K --> L;
```

## Flujo 2: Planificar un Viaje (A -> B)

```mermaid
flowchart TD
    subgraph Ingreso de Datos
        A[Pantalla: Inicio (Mapa)] --> B(Acción: Toca barra "Adónde vas?");
        B --> C[Pantalla: Búsqueda (Inputs)\nOrigen: "Tu Ubicación (Actual)"\nDestino: (vacío)];

        C --> D{¿Usuario cambia Origen?};
        D -- "Sí" --> E[Pantalla: Seleccionar Origen\n(Buscar, Elegir en mapa)];
        E --> F(Acción: Selecciona "Plaza de Armas");
        F --> G[Pantalla: Búsqueda (Inputs)\nOrigen: "Plaza de Armas"\nDestino: (vacío)];

        D -- "No (Usa Ubicación Actual)" --> G;

        G --> H(Acción: Escribe y selecciona "Destino"\nEj: "UANCV");
        H --> I(Acción: Toca botón "Buscar");
    end

    subgraph Cálculo y Resultados
        I --> J{Sistema: Calcula rutas A->B};

        J -- "Fallo (Sin rutas)" --> K[Pantalla: Resultados (Vacía)\n"No se encontraron rutas directas.\nIntenta con otro destino."];
        K --> L(Acción: Toca "Atrás");
        L --> C;

        J -- "Éxito (Rutas encontradas)" --> M[Pantalla: Resultados (Lista)\n"Rutas sugeridas (1-3 opciones)"];
        M(Opción 1: Línea 10) --> N(Acción: Toca Opción 1);
        M(Opción 2: Línea 15) --> N;

        N --> O[Pantalla: Detalle de Viaje (Navegación)\n(Muestra mapa A->B y pasos)];
        O(Pasos:\n1. Caminar a Paradero X\n2. Tomar Línea 10\n3. Bajar en Paradero Y...);
        O --> P(Fin del Flujo);
    end
```

## Flujo 3: Exploración de Rutas (Biblioteca)

```mermaid
flowchart TD
    A[Pantalla: Inicio (Mapa)] --> B(Acción: Toca pestaña "Explorar");
    B --> C[Pantalla: Explorar (Lista)\n(Muestra Barra de Búsqueda + Lista completa de líneas)];

    C --> D{¿Usuario usa Búsqueda?};
    D -- "Sí" --> E(Acción: Escribe "Línea 10");
    E --> F[Pantalla: Explorar (Lista Filtrada)\n(Solo muestra "Línea 10")];

    D -- "No (Navega la lista)" --> G(Acción: Toca "Línea 10");
    F --> G;

    G --> H[Pantalla: Detalle de Ruta (Mapa)\n(Muestra mapa con trazado COMPLETO de Línea 10)];
    H(Panel Info:\n"Línea 10" | Ícono "Guardar" [Futuro]);

    H --> I(Acción: Toca "Atrás");
    I --> C;
    H --> J(Fin del Flujo);
```
