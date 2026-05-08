---
title: "Gestión de Flotas UAS"
tags: [gestion-flotas, uas, operaciones, saas, modulos-canonicos]
source_count: 1
---

# Gestión de Flotas UAS

## Definición

Conjunto de procesos operacionales, técnicos y normativos para administrar un conjunto de aeronaves no tripuladas (UAS) a lo largo de su ciclo de vida completo. Abarca planificación de misiones, mantenimiento de aeronaves, gestión de personal habilitado, control de inventario, registro de vuelos y cumplimiento normativo.

## Módulos canónicos de U-Log

| Módulo                     | Funciones principales                                            | Estado de definición    |
| -------------------------- | ---------------------------------------------------------------- | ----------------------- |
| **Vuelos / Operaciones**   | Planificación, despacho, checklists, registro de misiones        | Identificado en pizarra |
| **Mantenimiento**          | MTX preventivo/correctivo, ciclo de vida de componentes, alertas | Pendiente de definir    |
| **Personal**               | Pilotos, licencias, capacitaciones, aptitud médica, historial    | Pendiente de definir    |
| **Inventario**             | Drones, baterías, payloads, piezas de repuesto                   | Pendiente de definir    |
| **Cumplimiento Normativo** | Documentación, autorizaciones AESA, auditorías, seguros          | Identificado en pizarra |
| **Logbooks**               | Registro obligatorio de vuelos (EASA) — innovación principal     | Identificado en pizarra |

> ⚠️ **Alerta de dependencia**: Los módulos de Mantenimiento y Personal no están definidos todavía. El módulo de Mantenimiento es dependiente del módulo de Inventario (ciclo de vida de baterías, horas de vuelo por componente). El módulo de Personal es dependiente del módulo de Vuelos (asignación de pilotos a misiones). ¿Se desean definir estos módulos siguiendo los estándares de DroneSuite?

## Jerarquía funcional

```
Módulo
  └─ Funcionalidad
       └─ User Story
            └─ Campos de Datos
```

Ejemplo aplicado a LOG:
```
Módulo: Logbooks
  └─ Funcionalidad: Generación automática de logbook
       └─ User Story: "Como operador, quiero que mi vuelo quede registrado
          automáticamente al finalizar la misión, sin introducir datos manualmente."
            └─ Campos: fecha, aeronave (S/N), piloto, coordenadas, duración,
               tipo operación, condiciones meteorológicas, incidencias
```

## Estándar del sector

Las plataformas líderes (DroneSuite, AirData UAV, DroneDeploy) cubren estos módulos con distinto nivel de profundidad. U-Log se diferencia por:
1. Integración nativa con [[entidades/dji-flighthub]] para automatizar el módulo LOG
2. UX "Dark Cockpit" con menor carga cognitiva
3. Diseño EASA-native desde el primer día

## Fuentes que lo mencionan

- [[fuentes/esquema-inicial-whiteboard]]

## Perspectivas distintas

- **DroneSuite**: énfasis en compliance y documentación centralizada
- **U-Log**: énfasis en integración con datos reales de vuelo para reducir carga manual

## Contradicciones detectadas

Ninguna aún.
