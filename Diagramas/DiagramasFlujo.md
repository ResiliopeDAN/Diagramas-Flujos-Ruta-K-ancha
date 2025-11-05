# Diagramas de Flujo - Ruta K'ancha

Este documento presenta los diagramas de flujo para los tres flujos principales del prototipo de la aplicación Ruta K'ancha. Cada diagrama está definido utilizando la sintaxis Mermaid (flowchart TD).

## Flujo 1: Onboarding (Carrusel de Bienvenida)

```mermaid
flowchart TD
    ob_inicio["Inicio: el usuario abre la app por primera vez"] --> ob_slide1["Pantalla: Bienvenida (Slide 1)<br/>Bienvenido a Ruta K'ancha"]
    ob_slide1 --> ob_accion_desliza1["Acción: el usuario desliza"]
    ob_accion_desliza1 --> ob_slide2["Pantalla: Valor 1 (Slide 2)<br/>Encuentra tu ruta más rápida"]
    ob_slide2 --> ob_accion_desliza2["Acción: el usuario desliza"]
    ob_accion_desliza2 --> ob_slide3["Pantalla: Valor 2 (Slide 3)<br/>Ahorra tiempo y dinero"]
    ob_slide3 --> ob_comenzar["Acción: toca «Comenzar»"]
    ob_comenzar --> ob_popup["Pop-up: solicitud de permiso de ubicación<br/>Ruta K'ancha necesita tu ubicación..."]

    ob_popup --> ob_decision{Acción: el usuario elige permiso}
    ob_decision -- "Permitir (recomendado)" --> ob_gps_on["Estado del sistema: GPS activado"]
    ob_decision -- "Solo esta vez" --> ob_gps_on
    ob_decision -- "Rechazar" --> ob_gps_off["Estado del sistema: GPS desactivado"]

    ob_gps_on --> ob_fin["Fin: ir a la pantalla principal"]
    ob_gps_off --> ob_fin
```

## Flujo 2: Planificar un Viaje (A -> B)

```mermaid
flowchart TD
    subgraph plan_datos [Ingreso de datos]
        plan_inicio["Pantalla: inicio (mapa)"] --> plan_barra["Acción: toca la barra «¿Adónde vas?»"]
        plan_barra --> plan_inputs["Pantalla: búsqueda (inputs)<br/>Origen: tu ubicación (actual)<br/>Destino: vacío"]

        plan_inputs --> plan_decision_origen{¿El usuario cambia el origen?}
        plan_decision_origen -- "Sí" --> plan_seleccion_origen["Pantalla: seleccionar origen<br/>Buscar o elegir en el mapa"]
        plan_seleccion_origen --> plan_origen_plaza["Acción: selecciona «Plaza de Armas»"]
        plan_origen_plaza --> plan_inputs_actualizados["Pantalla: búsqueda (inputs)<br/>Origen: Plaza de Armas<br/>Destino: vacío"]

        plan_decision_origen -- "No, usar ubicación actual" --> plan_inputs_actualizados

        plan_inputs_actualizados --> plan_destino["Acción: escribe y selecciona destino<br/>Ejemplo: UANCV"]
        plan_destino --> plan_buscar["Acción: toca el botón «Buscar»"]
    end

    subgraph plan_resultados [Cálculo y resultados]
        plan_buscar --> plan_calculo{Sistema: calcula rutas A → B}

        plan_calculo -- "Fallo: sin rutas" --> plan_sin_rutas["Pantalla: resultados (vacía)<br/>No se encontraron rutas directas.<br/>Intenta con otro destino."]
        plan_sin_rutas --> plan_regresar["Acción: toca «Atrás»"]
        plan_regresar --> plan_inputs

        plan_calculo -- "Éxito: rutas encontradas" --> plan_lista_rutas["Pantalla: resultados (lista)<br/>Rutas sugeridas (1-3 opciones)"]
        plan_lista_rutas --> plan_opcion1["Opción 1: Línea 10"]
        plan_lista_rutas --> plan_opcion2["Opción 2: Línea 15"]

        plan_opcion1 --> plan_detalle_accion["Acción: toca una opción"]
        plan_opcion2 --> plan_detalle_accion

        plan_detalle_accion --> plan_detalle_viaje["Pantalla: detalle de viaje (navegación)<br/>Muestra mapa A → B y pasos"]
        plan_detalle_viaje --> plan_pasos["Pasos:<br/>1. Caminar al paradero X<br/>2. Tomar la Línea 10<br/>3. Bajar en el paradero Y..."]
        plan_pasos --> plan_fin["Fin del flujo"]
    end
```

## Flujo 3: Exploración de Rutas (Biblioteca)

```mermaid
flowchart TD
    exp_inicio["Pantalla: inicio (mapa)"] --> exp_pestana["Acción: toca la pestaña «Explorar»"]
    exp_pestana --> exp_lista["Pantalla: explorar (lista)<br/>Barra de búsqueda y listado completo"]

    exp_lista --> exp_decision_busqueda{¿El usuario usa la búsqueda?}
    exp_decision_busqueda -- "Sí" --> exp_escribe_busqueda["Acción: escribe «Línea 10»"]
    exp_escribe_busqueda --> exp_lista_filtrada["Pantalla: explorar (lista filtrada)<br/>Solo muestra «Línea 10»"]

    exp_decision_busqueda -- "No, navegar la lista" --> exp_seleccion_lista["Acción: toca «Línea 10»"]
    exp_lista_filtrada --> exp_seleccion_lista

    exp_seleccion_lista --> exp_detalle_ruta["Pantalla: detalle de ruta (mapa)<br/>Trazado completo de la Línea 10"]
    exp_detalle_ruta --> exp_panel_info["Panel informativo:<br/>Línea 10 | ícono «Guardar» (futuro)"]

    exp_detalle_ruta --> exp_atras["Acción: toca «Atrás»"]
    exp_atras --> exp_lista
    exp_detalle_ruta --> exp_fin["Fin del flujo"]
```
