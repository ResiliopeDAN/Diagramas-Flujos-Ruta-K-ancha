```mermaid
graph TD

%% Actores Externos
App(Aplicación Móvil del Usuario)
Admin(Panel de Administración)
GPS[Fuentes de Datos en Tiempo Real (GPS)]

%% Backend
subgraph Supabase [Backend de Supabase]
direction TB

Auth[Supabase Auth]
API[APIs (RESTful / GraphQL)]
FN[Supabase Functions (Lógica / Ingesta)]
RT[Supabase Realtime (WebSockets)]

subgraph DB_Container [Base de Datos]
DB[(PostgreSQL)]
GIS[(PostGIS)]
DB --- GIS
end

Auth -->|Gestiona usuarios| DB
API -->|Acceso a datos| DB
FN -->|Procesa/Inserta datos| DB
DB -- Notifica cambios --> RT
end

%% Flujos
App -->|Login/Registro| Auth
App -->|Consulta datos (rutas, paradas)| API
App -->|Ejecuta lógica (ej. calcular ruta)| FN
RT -- Difusión de ubicaciones --> App

GPS -->|Envía datos de ubicación| FN

Admin -->|Gestión de datos (CRUD)| API
Admin -->|Gestión de usuarios| Auth
```