# Ecosistema IA para Atención de Clientes

## Descripción General

Este proyecto implementa un ecosistema de automatización inteligente utilizando n8n, OpenAI GPT-4o-mini, Gmail y Airtable para la gestión automatizada de correos electrónicos de atención al cliente.

La solución permite:

- Obtener correos electrónicos desde Gmail.
- Analizar el contenido mediante Inteligencia Artificial.
- Clasificar automáticamente cada interacción.
- Asignar una prioridad.
- Generar una respuesta sugerida.
- Registrar la información en Airtable.
- Solicitar aprobación humana antes de ejecutar una acción crítica.
- Registrar errores para garantizar trazabilidad y resiliencia.

---

# Objetivos del Proyecto

- Automatizar el procesamiento inicial de correos electrónicos.
- Reducir tareas manuales repetitivas.
- Implementar Inteligencia Artificial en un flujo real de negocio.
- Incorporar mecanismos Human-in-the-Loop.
- Registrar errores e incidencias para auditoría y seguimiento.
- Construir un Dashboard operativo para monitorear las interacciones procesadas.

---

# Arquitectura Tecnológica

## Orquestación

- n8n

## Inteligencia Artificial

- OpenAI GPT-4o-mini

## Fuente de Datos

- Gmail

## Base de Datos

- Airtable

## Human-in-the-Loop

- Gmail Send and Wait for Response

---

# Workflow Implementado

```text
TRG_REVISION_CORREO
        ↓
GMAIL_OBTENER_CORREOS
        ↓
SET_DATOS_EMAIL
        ↓
FORMATEAR_FECHA
        ↓
OPENAI_ANALIZAR_CORREO
        ↓
IF (Validación)
        ↓
AIRTABLE_GUARDAR_INTERACCION
        ↓
SOLICITAR_APROBACION_HUMANA
        ↓
UPDATE RECORD
        ↓
MARK A MESSAGE AS READ
```

---

# Gestión de Errores

El workflow incorpora una ruta de error específica para registrar incidencias durante el procesamiento.

```text
OPENAI_ANALIZAR_CORREO
        ↓
IF
        ↓
AIRTABLE_GUARDAR_ERROR
```

Los errores se almacenan mediante el campo:

```text
Logs_Errores
```

---

# Human-in-the-Loop

Antes de completar el proceso, el workflow requiere una validación humana utilizando:

```text
Send and Wait for Response
```

Las decisiones posibles son:

```text
Aprobado
Rechazado
```

La respuesta actualiza automáticamente el estado del registro en Airtable.

---

# Base de Datos

Tabla principal:

```text
Interacciones
```

Campos implementados:

```text
correo_id
mensaje
thread_id
fecha
estado
categoria_ia
prioridad_ia
respuesta_ia
Logs_Errores
```

---

# Dashboard de Control

Se implementó un Dashboard utilizando Airtable Interfaces para visualización operativa interna.

La fuente de información es la tabla:

```text
Interacciones
```

Indicadores monitorizados:

- Total de interacciones.
- Estado de procesamiento.
- Categorías generadas por IA.
- Prioridades asignadas por IA.
- Registros de errores.
- Seguimiento temporal de interacciones.

## Shared View Pública

Para cumplir el requisito de acceso público solicitado por la consigna, se publicó la siguiente Shared View de Airtable:

**Dashboard_Control**

[Acceder a Dashboard_Control](https://airtable.com/appOwIAfHolX1vPob/shrvna2fkQpMPl6KH)

---

# Limitación Documentada

Durante la implementación se creó una Interface de Airtable denominada:

```text
Tablero
```

Esta Interface contiene indicadores y gráficos construidos sobre la tabla Interacciones.

Sin embargo, Airtable restringe la publicación pública de Interfaces para el tipo de licencia utilizado durante el desarrollo del proyecto.

Por este motivo:

- La Interface permanece disponible únicamente para uso interno.
- No fue posible generar un enlace público de la Interface.
- El requisito académico de acceso público se resolvió utilizando una Shared View de Airtable.
- Esta limitación corresponde al plan de licencia utilizado y no a una limitación técnica del workflow desarrollado.

Con fines de transparencia y documentación técnica, no se declara ninguna URL pública de la Interface porque dicha funcionalidad no se encuentra habilitada en la licencia disponible.

---

# Optimización de Costes

Modelo implementado:

```text
GPT-4o-mini
```

Funciones realizadas por el modelo:

- Clasificación de correos.
- Asignación de prioridad.
- Generación de respuesta sugerida.

La elección de GPT-4o-mini permite utilizar un único modelo para todo el flujo, reduciendo complejidad operativa y costes computacionales.

---

# Seguridad y Resiliencia

La solución incorpora:

- Registro de errores.
- Human-in-the-Loop.
- Validación previa a acciones críticas.
- Trazabilidad mediante Airtable.
- Prevención de reprocesamientos mediante:
  
```text
MARK A MESSAGE AS READ
```

---
# Lógica del Flujo

La lógica completa del sistema fue desarrollada en n8n.

El flujo incluye:

- Obtención automática de correos desde Gmail.
- Normalización de datos.
- Clasificación mediante OpenAI GPT-4o-mini.
- Gestión de errores.
- Registro en Airtable.
- Human-in-the-Loop mediante aprobación humana.
- Actualización de estados.
- Prevención de reprocesamientos.

El archivo técnico exportado desde n8n se encuentra en:


# Autor

**Julio Enrique Rodríguez Angulo**

Trabajo Final  
Automatización e Inteligencia Artificial

---

Proyecto desarrollado para la entrega final:

**Ecosistema IA Autónomo para Atención de Clientes**
