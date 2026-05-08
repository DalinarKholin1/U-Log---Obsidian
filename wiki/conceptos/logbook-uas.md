---
title: "Logbook UAS"
tags: [logbook, registro-vuelos, easa, cumplimiento-normativo, integracion, innovacion]
source_count: 1
---

# Logbook UAS

## Definición

Registro obligatorio de vuelos de aeronaves no tripuladas requerido por [[entidades/easa]] (EU 2019/947) para operaciones en categoría Specific. Documenta cada misión con datos de piloto, aeronave, ubicación, duración e incidencias. Es el artefacto de cumplimiento normativo más frecuente en la operación diaria de un operador UAS profesional.

## Campos mínimos EASA

| Campo | Tipo de dato | Fuente automática (FlightHub) | Obligatorio |
|---|---|---|---|
| Fecha / hora inicio-fin | Timestamp UTC | ✅ | ✅ |
| Piloto al mando | ID de usuario | Parcial (si piloto registrado en FH2) | ✅ |
| Aeronave (número de serie) | String | ✅ | ✅ |
| Área de operación | Polígono / coordenadas | ✅ (track GPS) | ✅ |
| Duración del vuelo | Minutos | ✅ | ✅ |
| Tipo de operación | VLOS / BVLOS / etc. | ❌ (manual) | ✅ |
| Incidencias | Texto libre + clasificación | ❌ (manual) | ✅ |
| Condiciones meteorológicas | METAR / manual | ❌ (API meteo opcional) | Recomendado |
| Batería utilizada | ID batería | Parcial (si registrada en FH2) | Recomendado |

**Conclusión**: FlightHub 2 cubre ~60-70% de los campos. El formulario post-vuelo de U-Log pide solo los campos restantes → reducción de carga manual estimada en 80%.

## Flujo de generación en U-Log

```
Vuelo finalizado en DJI FlightHub
       ↓
API FlightHub 2 → U-Log (webhook o polling)
       ↓
Ingesta automática de telemetría
       ↓
Pre-relleno de logbook (60-70% campos)
       ↓
Notificación al piloto: "Revisa y completa tu logbook"
       ↓
Formulario mínimo (2-3 campos restantes)
       ↓
Firma digital del piloto
       ↓
Logbook finalizado y archivado (PDF + datos estructurados)
```

## Valor para el operador

| Situación actual (sin U-Log) | Con U-Log |
|---|---|
| Rellenar logbook manual: 5-10 min/vuelo | Completar formulario mínimo: 1-2 min/vuelo |
| Formato Excel / papel → difícil auditar | Formato digital estructurado → exportable EASA |
| Datos de vuelo en FlightHub, logbook en Excel | Todo integrado en una plataforma |
| Riesgo de olvido / error de datos | Datos de telemetría reales → mayor precisión |

## Fuentes que lo mencionan

- [[fuentes/esquema-inicial-whiteboard]]

## Perspectivas distintas

- **Regulador (EASA/AESA)**: documento de compliance, soporte para auditorías e investigación de accidentes
- **Operador**: carga administrativa que U-Log elimina en su mayoría
- **Piloto**: prueba de experiencia acumulada (horas totales de vuelo, historial de aeronaves)
- **Aseguradoras**: fuente de datos para cálculo de riesgo / primas

## Contradicciones detectadas

Ninguna aún.
