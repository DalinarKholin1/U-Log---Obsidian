---
title: "EASA"
type: regulacion
tags: [regulacion, easa, uas, europa, cumplimiento-normativo, logbook]
---

# EASA — European Union Aviation Safety Agency

## Descripción

Agencia de la Unión Europea responsable de la seguridad aérea civil, incluyendo la regulación de operaciones UAS. Establece el marco normativo bajo el cual operan los clientes de U-Log y define los requisitos de registro que el módulo LOG debe satisfacer.

## Regulaciones clave para UAS

| Regulación | Contenido | Impacto directo en U-Log |
|---|---|---|
| **EU 2019/947** | Operaciones UAS — categorías Open/Specific/Certified | Base del módulo Cumplimiento Normativo |
| **EU 2019/945** | Requisitos de diseño y fabricación UAS | Gestión de activos — campos del drone |
| **EU 2021/664** | U-Space / UTM | Integración futura con gestión de espacio aéreo |
| **AMC/GM to Part-UAS** | Material de orientación operacional | Checklists, procedimientos pre/post vuelo |

## Categorías operacionales

| Categoría | Descripción | Perfil de cliente U-Log |
|---|---|---|
| **Open** | Bajo riesgo, sin autorización previa | Secundario |
| **Specific** | Requiere SORA o PDRA | **Mercado objetivo principal** |
| **Certified** | Alto riesgo, equivalente aviación tripulada | Futuro (Fase 3) |

## Requisitos mínimos de logbook (Specific)

Campos obligatorios definidos por EASA que U-Log debe cubrir:
- Fecha y hora de inicio/fin
- Piloto al mando (identificación)
- Aeronave (número de serie)
- Área de operación (coordenadas)
- Duración del vuelo
- Tipo de operación (VLOS/BVLOS)
- Incidencias registradas

## Aparece en

- Aplicable a todos los módulos de U-Log (transversal)

## Relaciones

- [[entidades/aesa]] — autoridad nacional española bajo marco EASA
- [[conceptos/metodologia-sora]] — metodología de evaluación de riesgos para categoría Specific
- [[conceptos/logbook-uas]] — requisito de registro definido por EASA

## Notas

Los campos obligatorios del logbook EASA son inputs directos al modelo de datos del módulo LOG. La conformidad EASA es un requisito no negociable y también una herramienta de marketing ("logbook certificado EASA").
