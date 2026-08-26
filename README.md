# Ecosistema IA Autónomo para Atención de Clientes

## Descripción del Proyecto

Sistema de automatización inteligente desarrollado con n8n, Gmail, OpenAI GPT-4o-mini y Airtable para la gestión, clasificación y seguimiento de correos electrónicos mediante Inteligencia Artificial.

El proyecto implementa:

- Automatización de recepción de correos.
- Clasificación mediante IA.
- Registro y seguimiento en Airtable.
- Human-in-the-Loop (aprobación humana).
- Gestión centralizada de errores.
- Dashboard de monitoreo y control.

---

# Tecnologías Utilizadas

- n8n
- Gmail
- OpenAI GPT-4o-mini
- Airtable
- GitHub
- Lucidchart

---

# Arquitectura del Sistema

## Workflow Principal

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

### Funciones

- Recepción de correos desde Gmail.
- Formateo y normalización de datos.
- Clasificación mediante OpenAI.
- Registro de información en Airtable.
- Supervisión humana antes de continuar el proceso.

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

### Funciones

- Captura automática de errores.
- Registro centralizado de incidencias.
- Auditoría y trazabilidad.

---

# Lógica del Flujo (n8n)

La rúbrica solicita la entrega de la lógica del flujo en formato JSON.

Los workflows implementados se encuentran en:

```text
workflow/
```

### Workflow Principal

Archivo:

```text
workflow/WF_ATENCION_CLIENTE_IA.json
```

Contiene:

- Trigger de revisión de correo.
- Integración Gmail.
- Procesamiento OpenAI.
- Escritura en Airtable.
- Human-in-the-Loop.

---

### Workflow de Gestión de Errores

Archivo:

```text
workflow/WF_ERROR_HANDLER.json
```

Contiene:

- Error Trigger.
- Registro automático en Airtable.
- Gestión centralizada de incidentes.

---

## Importación de Workflows

Para reutilizar los workflows:

1. Abrir n8n.
2. Seleccionar Import Workflow.
3. Importar el archivo JSON correspondiente.
4. Configurar las credenciales:
   - Gmail
   - OpenAI
   - Airtable
5. Activar los workflows.

---

# Human-in-the-Loop

Se implementó utilizando:

```text
Send and Wait for Response
```

Opciones:

- Approve
- Decline

La ejecución permanece detenida hasta recibir una decisión humana.

Objetivos:

- Validación humana.
- Reducción de errores.
- Control operativo.

---

# Gestión de Errores (Resiliencia)

Workflow:

```text
WF_ERROR_HANDLER
```

Configuración:

```text
Error Trigger
↓
Airtable
↓
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

KPIs definidos:

- Total Interacciones
- Total Errores
- Errores Abiertos
- Pendientes
- Tasa de Error

Fórmula:

```text
Tasa Error (%) =
(Total Errores / Total Interacciones) * 100
```

## Limitación de Licencia

La licencia utilizada de Airtable no permite publicar la interfaz mediante la opción "Compartir en la Web".

Por este motivo se incluyen:

- Evidencias del dashboard.
- Shared Views cuando estén disponibles.
- Capturas de respaldo en el repositorio.

---

# Documentación Incluida

Carpeta:

```text
documentos/
```

Contenido:

- Arquitectura_Sistema.pdf
- Manual_Operativo_Datos.pdf
- Matriz_Costos.pdf
- Seguridad_Resiliencia.pdf
- Dashboard_Control.pdf

---

# Evidencias

Carpeta:

```text
evidencias/
```

Contenido:

- flujo_n8n.png
- human_in_the_loop.png
- error_handler.png
- error_logs.png
- dashboard_kpi.png

---

# Estructura del Repositorio

```text
Entrega_Final_Ecosistema_IA
│
├── documentos/
│   ├── Arquitectura_Sistema.pdf
│   ├── Manual_Operativo_Datos.pdf
│   ├── Matriz_Costos.pdf
│   ├── Seguridad_Resiliencia.pdf
│   └── Dashboard_Control.pdf
│
├── workflow/
│   ├── WF_ATENCION_CLIENTE_IA.json
│   └── WF_ERROR_HANDLER.json
│
├── evidencias/
│   ├── flujo_n8n.png
│   ├── human_in_the_loop.png
│   ├── error_handler.png
│   ├── error_logs.png
│   └── dashboard_kpi.png
│
├── enlaces/
│   └── enlaces.md
│
└── README.md
```

---

# Autor

Julio Enrique Rodríguez Angulo

Proyecto desarrollado para la entrega final:

**Ecosistema IA Autónomo para Atención de Clientes**
