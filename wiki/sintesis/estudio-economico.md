---
title: "Estudio Económico — Costes, Ingresos y Financiación de U-Log"
date: 2026-05-08
query_origin: "Análisis económico para la concepción y arranque de U-Log"
tags: [economico, costes, ingresos, financiacion, ayudas, saas]
fuentes_citadas: [esquema-inicial-whiteboard]
---

# Estudio Económico — Costes, Ingresos y Financiación de U-Log

## 1. Estructura de Costes

### Costes Directos (identificados en pizarra)

| Categoría | Descripción | Estimación mensual (fase MVP) |
|---|---|---|
| **Infraestructura Cloud** | AWS o Azure: compute, storage, CDN, backups | €300-800/mes |
| **DJI FlightHub 2 API** | Suscripción empresarial para acceso a API | €100-300/mes (est.) |
| **Servicios SaaS de terceros** | Auth0/Clerk (auth), Sentry (errores), Datadog (monitoring) | €200-500/mes |
| **Dominio + SSL + email corporativo** | Infraestructura básica | €50-100/mes |
| **Total costes directos MVP** | | **~€650-1,700/mes** |

### Costes Indirectos (identificados en pizarra)

| Categoría | Descripción | Estimación |
|---|---|---|
| **Tiempo propio** | Horas de desarrollo, gestión, ventas del founding team | Coste de oportunidad — cuantificar en horas/semana |
| **Tiempo ajeno** | Freelancers, consultores (diseño, legal, fiscal) | €3,000-10,000 (fases puntuales) |
| **Movilidad** | Visitas a clientes, eventos del sector, ferias | €200-500/mes en fase de ventas |
| **Legal y registro** | Constitución de sociedad, contratos, RGPD | €2,000-4,000 (one-time) |
| **Certificaciones** | ISO 27001 (futuro), ENS (futuro B2G) | €10,000-30,000 (mediano plazo) |

### Proyección de costes por fase

| Fase | Duración | Coste mensual total (est.) |
|---|---|---|
| Pre-MVP (desarrollo) | 4-8 meses | €1,500-3,000 |
| Beta / validación | 4-6 meses | €2,000-4,000 |
| Crecimiento | Año 2 | €5,000-15,000 |

---

## 2. Modelo de Ingresos

### Modelo SaaS por suscripción mensual

| Plan | Descripción | Precio/mes | Target |
|---|---|---|---|
| **Starter** | Hasta 3 aeronaves, 1 piloto, logbooks ilimitados | €99 | Operadores individuales |
| **Professional** | Hasta 10 aeronaves, 5 pilotos, informes + API | €249 | PYME inspección |
| **Business** | Hasta 30 aeronaves, usuarios ilimitados, SLA | €599 | Empresas medianas |
| **Enterprise** | Ilimitado, onboarding dedicado, SLA contractual | Precio negociado | Grandes operadores / B2G |

### Proyección de ingresos (modelo conservador)

| Mes | Clientes | ARR estimado | MRR estimado |
|---|---|---|---|
| 6 | 5 (beta) | €0 (gratuito) | €0 |
| 12 | 20 | €36K | €3K |
| 18 | 60 | €108K | €9K |
| 24 | 120 | €240K | €20K |
| 36 | 300 | €720K | €60K |

> Basado en pricing medio de €200/cliente/mes. Modelo conservador — pendiente de validar con early adopters.

### Métricas SaaS objetivo

| Métrica | Objetivo año 1 | Objetivo año 2 |
|---|---|---|
| MRR (Monthly Recurring Revenue) | €3,000 | €20,000 |
| Churn mensual | <3% | <2% |
| CAC (Coste de Adquisición) | <€500 | <€300 |
| LTV (Lifetime Value) | >€2,000 | >€4,000 |
| LTV/CAC ratio | >4x | >10x |

---

## 3. Ayudas y Subvenciones Disponibles

### España

| Programa | Organismo | Dotación típica | Requisito | Compatibilidad U-Log |
|---|---|---|---|---|
| **CDTI Neotec** | CDTI (Ministerio Ciencia) | €175,000-250,000 préstamo participativo | Empresa innovadora <6 años | Alta — SaaS con innovación técnica |
| **CDTI Innvierte** | CDTI | Co-inversión con VC | Necesita co-inversor privado | Media-Alta |
| **CDTI Proyectos I+D** | CDTI | €150,000-500,000 | Proyecto I+D definido | Alta (integración FlightHub + IA) |
| **Kit Digital (Digitalización)** | Red.es | €2,000-12,000 | Para clientes PYME de U-Log | Indirecto — U-Log como solución Kit Digital |
| **Ayudas ENISA** | ENISA | €75,000-1,500,000 préstamo | Empresa innovadora | Alta |
| **ICEX Next** | ICEX | €30,000-90,000 | Para internacionalización | Relevante en Fase 3 |

### Europeas

| Programa | Organismo | Dotación típica | Relevancia |
|---|---|---|---|
| **EIC Accelerator** | Comisión Europea | Hasta €2.5M (grant) + €15M (equity) | Alta — innovación disruptiva en sector estratégico |
| **Horizon Europe** | Comisión Europea | Variable (proyectos consorcio) | Media — requiere consorcio multi-país |
| **ESA BIC Spain** | ESA + CDTI | €50,000 + servicios | Alta — sector aeroespacial, sede en Madrid/Barcelona |
| **EUSPA (Space data)** | EUSPA | Variable | Media — si se integra GNSS/Galileo en telemetría |

### Estrategia de financiación recomendada

```
Fase 1 (0-12 meses):  Bootstrapping + ENISA o CDTI Neotec
Fase 2 (12-24 meses): Ronda seed (€300K-€1M) + CDTI Proyectos I+D
Fase 3 (24-36 meses): Serie A + EIC Accelerator (si se cumplen requisitos)
```

---

## 4. Assets Necesarios

### Activos tangibles

| Asset | Descripción | Coste estimado | Timing |
|---|---|---|---|
| Portátiles de desarrollo | 1-2 MacBook Pro / Dev machines | €2,500-5,000 | Inmediato |
| Drones de prueba | 1-2 DJI Enterprise para desarrollo/demo | €3,000-8,000 | Pre-MVP |
| Cuenta AWS/Azure | Créditos de startup disponibles | €0 (créditos) → €500/mes | Inmediato |
| Cuentas DJI FlightHub 2 | Licencias para testing | €200-500/año | Pre-MVP |

### Activos intangibles

| Asset | Descripción | Timing |
|---|---|---|
| Marca registrada "U-Log" | Registro EUIPO (EU) | Antes de lanzamiento público |
| Dominio principal | u-log.io o u-log.aero | Inmediato |
| Código fuente (propiedad IP) | Contratos de cesión de IP con colaboradores | Antes de desarrollar |
| Primeras relaciones comerciales | Cartas de intención de early adopters | Pre-MVP |

---

## 5. Punto de Equilibrio

| Escenario | Clientes necesarios | MRR necesario |
|---|---|---|
| Break-even coste directo (<€2,000/mes) | ~10-15 clientes | €2,000/mes |
| Break-even con 1 FTE (€3,000 nómina) | ~25-30 clientes | €5,000/mes |
| Break-even con equipo 3 personas | ~75-100 clientes | €15,000/mes |

---

## Fuentes citadas

- [[fuentes/esquema-inicial-whiteboard]]
