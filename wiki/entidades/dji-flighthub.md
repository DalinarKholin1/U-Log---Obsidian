---
title: "DJI FlightHub 2"
type: sistema
tags: [dji, telemetria, gestion-flotas, integracion, flighthub, api]
---

# DJI FlightHub 2

## Descripción

DJI FlightHub 2 es la plataforma de gestión de vuelos de DJI para uso empresarial. U-Log la utiliza exclusivamente como **fuente de datos de telemetría**: al finalizar cada vuelo, la API de FlightHub provee los datos necesarios para generar automáticamente el log de ruta de vuelo, el logbook del piloto y el logbook del dron — sin entrada manual.

## Funcionalidades utilizadas en la integración U-Log

| Funcionalidad FlightHub 2         | Uso en U-Log                 | Módulo destino |
| --------------------------------- | ---------------------------- | -------------- |
| Registro automático de telemetría | Fuente de datos de vuelo     | LOG            |
| Historial de vuelos exportable    | Base de logbooks EASA        | LOG            |
| API REST (FlightHub 2)            | Punto de integración técnico | HUB/NODO       |

## Qué genera la integración

Al finalizar un vuelo en DJI FlightHub 2, U-Log extrae la telemetría y genera automáticamente tres artefactos:

| Artefacto | Contenido | Receptor |
|---|---|---|
| **Log de ruta de vuelo** | Track GPS completo, altitud, velocidad, duración | Módulo LOG / Missions |
| **Logbook del piloto** | Horas acumuladas, aeronave usada, área, fecha/hora | Módulo LOG / Personal |
| **Logbook del dron** | Horas de vuelo del aparato, ciclos de batería, ID | Módulo LOG / Fleet |

Los campos que FlightHub no provee (tipo de operación, incidencias, observaciones) se completan mediante formulario mínimo post-vuelo.

## Investigación de implementación API

> 🔲 **Tarea de investigación técnica prioritaria** — a completar antes del MVP.

Preguntas a resolver sobre la API de DJI FlightHub 2:

- [ ] ¿Qué endpoint/webhook notifica el fin de un vuelo? ¿Push o polling?
- [ ] ¿Qué campos de telemetría están disponibles por vuelo? (track GPS, altitud, velocidad, batería...)
- [ ] ¿La API devuelve datos del piloto asignado al vuelo o solo del drone?
- [ ] ¿Cuál es el formato de los datos de vuelo? (JSON, CSV, propietario...)
- [ ] ¿Existen rate limits que afecten a la sincronización en tiempo real?
- [ ] ¿Requiere la API credenciales por organización o existe un modo multi-tenant?
- [ ] ¿La versión gratuita de FlightHub 2 tiene acceso a la API o es solo de pago?
- [ ] ¿Existe un sandbox/entorno de pruebas oficial de DJI?

**Recursos de partida**:
- DJI FlightHub 2 API Documentation (requiere cuenta DJI Developer)
- DJI Developer Portal: developer.dji.com
- FlightHub 2 Enterprise: enterprise.dji.com/flighthub-2

## Riesgos de la integración

| Riesgo | Probabilidad | Mitigación |
|---|---|---|
| Lock-in de ecosistema DJI | Media | Implementar MAVLink genérico en paralelo |
| Cambio de API sin previo aviso | Baja-Media | Capa de abstracción + monitorización de changelog |
| FlightHub 2 requiere suscripción DJI | Alta | Coste a absorber en precio U-Log o trasladar al cliente |
| Cobertura limitada a drones DJI | Alta | Roadmap: integración con otros fabricantes vía MAVLink |

## Aparece en

- [[fuentes/esquema-inicial-whiteboard]] — mencionado como "Lock/logbooks" en zona de diferenciadores

## Relaciones

- [[entidades/dronesuite]] — competidor sin esta integración (gap que U-Log explota)
- [[conceptos/logbook-uas]] — artefacto principal generado por la integración
- [[conceptos/mavlink]] — protocolo para cobertura de drones no-DJI

## Notas

Prioridad técnica máxima en el roadmap. La prueba de concepto de la integración FlightHub API debe ser el primer artefacto técnico del proyecto. Ver [[sintesis/desarrollo-aplicacion]] para detalles técnicos.
