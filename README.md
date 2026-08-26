# Ecosistema IA Autónomo para Atención de Clientes

## Descripción del Proyecto

Este proyecto implementa un ecosistema de automatización basado en Inteligencia Artificial para la gestión y clasificación de correos electrónicos mediante n8n, Gmail, OpenAI GPT-4o-mini y Airtable.

El objetivo es automatizar la recepción, clasificación, priorización y gestión de solicitudes recibidas por correo electrónico, incorporando mecanismos de supervisión humana (Human-in-the-Loop) y gestión de errores (Resiliencia).

---

# Arquitectura General

El sistema está compuesto por dos workflows principales:

## Workflow Operativo

WF_ATENCION_CLIENTE_IA

```text
TRG_REVISION_CORREO
↓
GMAIL_OBTENER_CORREOS
↓
ESTABLECER_DATOS_CORREO_ELECTRONICO
↓
FORMATEAR_FECHA
↓
OPENAI_ANALIZAR_CORREO
↓
INTERACCION_DE_AIRTABLE_GUARDAR
↓
SOLICITAR_APROBACION_HUMANA
↓
APPROVE / DECLINE
```

Funciones principales:

- Recepción de correos desde Gmail.
- Normalización de datos.
- Clasificación mediante OpenAI.
- Almacenamiento en Airtable.
- Validación humana previa.

---

## Workflow de Resiliencia

WF_ERROR_HANDLER

```text
ERROR_TRIGGER
↓
REGISTRAR_ERROR
↓
LOGS_ERRORES
```

Funciones principales:

- Captura automática de fallos.
- Registro estructurado de incidencias.
- Auditoría y trazabilidad de errores.

---

# Tecnologías Utilizadas

- n8n
- Gmail API
- OpenAI GPT-4o-mini
- Airtable
- GitHub
- Lucidchart

---

# Human-in-the-Loop

El sistema incorpora validación humana mediante:

```text
Send and Wait for Response
```

Opciones disponibles:

- Approve
- Decline

La ejecución se detiene hasta recibir una decisión humana.

Objetivos:

- Evitar respuestas automáticas sin supervisión.
- Incrementar la calidad de las decisiones.
- Reducir riesgos operativos.

---

# Gestión de Errores (Resiliencia)

Se implementó un workflow independiente:

```text
WF_ERROR_HANDLER
```

activado mediante:

```text
Error Trigger
```

Los errores son almacenados en:

```text
Logs_Errores
```

Información registrada:

- error_id
- workflow
- nodo_error
- mensaje_error
- fecha_error
- estado_error
- origen

---

# Base de Datos

Base:

```text
Atencion_Cliente_IA
```

## Tabla Interacciones

Campos principales:

- correo_id
- thread_id
- mensaje
- fecha
- estado
- categoria_ia
- prioridad_ia
- respuesta_ia

## Tabla Logs_Errores

Campos principales:

- error_id
- workflow
- nodo_error
- mensaje_error
- fecha_error
- estado_error
- origen

---

# Dashboard de Control

KPIs implementados:

- Total Interacciones
- Total Errores
- Errores Abiertos
- Pendientes
- Tasa de Error

Fórmula:

```text
Tasa de Error (%) =
(Total Errores / Total Interacciones) * 100
```

## Limitación de licencia

La licencia utilizada de Airtable no permite publicar la interfaz Dashboard mediante la opción "Compartir en la Web".

Por este motivo se adjuntan:

- Evidencias visuales del dashboard.
- Shared Views cuando estén disponibles.
- Capturas de respaldo dentro del repositorio.

---

# Estructura del Repositorio

```text
docs/
│
├── Arquitectura_Sistema.pdf
├── Manual_Operativo_Datos.pdf
├── Matriz_Costos.pdf
├── Seguridad_Resiliencia.pdf
└── Dashboard_Control.pdf

workflow/
│
├── WF_ATENCION_CLIENTE_IA.json
└── WF_ERROR_HANDLER.json

evidencias/
│
├── flujo_n8n.png
├── human_in_the_loop.png
├── error_handler.png
├── error_logs.png
└── dashboard_kpi.png

enlaces/
│
└── enlaces.md
```

---

# Documentación Incluida

## Arquitectura

Documento PDF con:

- Triggers
- APIs
- Nodos de IA
- Router de aprobación
- Destinos de datos
- Workflow de errores

## Manual Operativo de Datos

Incluye:

- Esquema de tablas Airtable
- Estructuras JSON
- Flujo de datos entre sistemas

## Matriz de Costos

Justificación de selección de modelos:

- GPT-4o-mini
- Claude Sonnet (referencia)
- Batch API (propuesta)

Incluye simulación de ahorro estimado.

## Seguridad y Resiliencia

Incluye:

- Minimización de datos
- Human-in-the-Loop
- Error Handlers
- Auditoría de errores

---

# Autor

Julio Enrique Rodríguez Angulo

Proyecto académico desarrollado para la entrega final del módulo:

**Ecosistema IA Autónomo para Atención de Clientes**
``
