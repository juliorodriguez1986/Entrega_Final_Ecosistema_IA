# Ecosistema IA Autónomo para Atención de Clientes

## Descripción

Sistema de automatización construido con n8n, Gmail, OpenAI GPT-4o-mini y Airtable para la gestión y clasificación de correos electrónicos mediante IA.

## Tecnologías utilizadas

- n8n
- Gmail
- OpenAI GPT-4o-mini
- Airtable

## Arquitectura

El workflow principal realiza:

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

## Human-in-the-Loop

Implementado mediante:

- Send and Wait for Response
- Approve
- Decline

## Gestión de Errores

Workflow:

WF_ERROR_HANDLER

Error Trigger
↓
Registro automático en Logs_Errores

## Base de Datos

Base:

Atencion_Cliente_IA

Tablas:

- Interacciones
- Logs_Errores

## Evidencias

Ver carpeta evidencias/

## Workflows

Ver carpeta workflow/

## Documentación

Ver carpeta docs/
