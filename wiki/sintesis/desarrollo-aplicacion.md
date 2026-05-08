---
title: "Desarrollo de Aplicación — Requisitos Técnicos de Alto Nivel"
date: 2026-05-08
query_origin: "Definición de requisitos técnicos, stack y arquitectura para U-Log"
tags: [desarrollo, arquitectura, backend, frontend, ciberseguridad, infraestructura, saas]
fuentes_citadas: [esquema-inicial-whiteboard]
---

# Desarrollo de Aplicación — Requisitos Técnicos de Alto Nivel

## Principios de Diseño Técnico

1. **API-first**: toda funcionalidad expuesta vía API REST/GraphQL — facilita integraciones (FlightHub, UTM, terceros)
2. **EASA-native**: el modelo de datos se diseña desde el principio para cumplir campos requeridos por regulación
3. **Multi-tenancy**: cada organización tiene datos completamente aislados
4. **Mobile-ready**: los pilotos firman logbooks desde el campo — la app debe funcionar en móvil
5. **Offline-tolerant**: los entornos de operación UAS pueden tener conectividad limitada

---

## 1. Arquitectura General

### Patrón: Microservicios con API Gateway

```
                          ┌─────────────────┐
                          │   Web App (SPA) │
                          │  React/Next.js  │
                          └────────┬────────┘
                                   │ HTTPS
                          ┌────────▼────────┐
                          │   API Gateway   │
                          │  (Kong / AWS)   │
                          └────┬──────┬─────┘
                               │      │
              ┌────────────────┤      ├────────────────┐
              │                │      │                │
    ┌─────────▼──┐   ┌─────────▼──┐  ┌▼───────────┐  ┌▼───────────┐
    │  Logbook   │   │  Fleet     │  │ Compliance │  │Integration │
    │  Service   │   │  Service   │  │  Service   │  │  Service   │
    │  (Go)      │   │  (Go)      │  │  (Go)      │  │  (Go/Py)   │
    └─────────┬──┘   └──────┬─────┘  └────┬───────┘  └─────┬──────┘
              │              │             │                 │
              └──────────────┴─────────────┘                │
                             │                              │
                    ┌────────▼────────┐             ┌───────▼───────┐
                    │  PostgreSQL     │             │ DJI FlightHub │
                    │  + TimescaleDB  │             │     API       │
                    └─────────────────┘             └───────────────┘
```

---

## 2. Stack Tecnológico

### Backend

| Componente | Tecnología recomendada | Razón |
|---|---|---|
| Lenguaje principal | **Go (Golang)** | Alto rendimiento, concurrencia nativa, despliegue simple, ecosistema cloud maduro |
| Alternativa / servicios IA | **Python** | Librerías de ML/IA para asistente contextual |
| Protocolo de comunicación interna | **gRPC + Protobuf** | Eficiencia inter-servicio, contratos tipados |
| Cola de mensajes | **NATS o RabbitMQ** | Procesamiento async de telemetría entrante |
| Base de datos principal | **PostgreSQL 16** | ACID, JSON nativo, extensiones GIS |
| Base de datos de telemetría | **TimescaleDB** (extensión PostgreSQL) | Time-series optimizado para datos de vuelo |
| Cache / sesiones | **Redis** | Sesiones, rate limiting, datos hot |

> **Safety-First**: Evitar Rust en el MVP — la curva de aprendizaje alarga el time-to-market innecesariamente. Go ofrece el 90% del rendimiento con el 20% de la complejidad. Rust puede reservarse para componentes de procesamiento de telemetría de alta frecuencia en fases posteriores.

### Frontend

| Componente | Tecnología | Razón |
|---|---|---|
| Framework | **Next.js 14+** (React) | SSR/SSG, App Router, ecosistema maduro |
| Lenguaje | **TypeScript** | Tipado estático — reduce bugs en formularios críticos |
| Estilos | **Tailwind CSS** | Diseño Dark Cockpit eficiente, componentes consistentes |
| Componentes UI base | **shadcn/ui** | Accesible, composable, personalizable |
| Gráficos / telemetría | **Recharts o Nivo** | Visualización de datos de vuelo |
| Mapas | **Mapbox GL JS o Leaflet** | Trayectorias de vuelo, áreas de operación |
| Estado global | **Zustand o Jotai** | Ligero, suficiente para el MVP |

### Mobile (para firma de logbooks en campo)

| Opción | Tecnología | Razón |
|---|---|---|
| Recomendada (MVP) | **PWA (Progressive Web App)** | Reutiliza el frontend web, no requiere app stores |
| Futura | **React Native** | App nativa si la experiencia móvil requiere más rendimiento |

---

## 3. Integración con DJI FlightHub 2

### Arquitectura de integración

```
DJI FlightHub 2
      │
      │  Webhook (event-driven) o Polling (cada N min)
      ▼
Integration Service (Go)
      │
      ├─ Validación y normalización de telemetría
      ├─ Detección de vuelo nuevo
      ├─ Mapeo a modelo de datos U-Log
      └─ Publicación en cola NATS
            │
            ▼
      Logbook Service
            │
            ├─ Pre-relleno automático de campos EASA
            ├─ Notificación al piloto: "Revisa y firma"
            └─ Archivado con hash SHA-256 (integridad)
```

### Campos cubiertos por FlightHub API

Ver [[conceptos/logbook-uas]] — tabla de campos y cobertura automática.

### Prioridad de desarrollo: Proof of Concept

El primer artefacto técnico del proyecto debe ser una PoC que demuestre:
1. Llamada exitosa a la API de FlightHub 2
2. Extracción de datos de un vuelo de prueba
3. Generación de un logbook borrador en formato U-Log

Este PoC valida la viabilidad técnica de la propuesta de valor central antes de invertir en la plataforma completa.

---

## 4. Entorno y Diseño de Interfaz

### Principios de UX (Dark Cockpit)

Ver [[sintesis/imagen-marca-u-log]] — sección Filosofía de Diseño.

### Pantallas críticas del MVP

| Pantalla | Módulo | Descripción |
|---|---|---|
| **Dashboard operacional** | Global | Estado de flota, alertas activas, vuelos del día |
| **Fleet overview** | Fleet | Listado de aeronaves con estado (operativa / MTX / inactiva) |
| **Logbook — lista** | Logbook | Vuelos del período, estado (firmado / pendiente / borrador) |
| **Logbook — detalle/firma** | Logbook | Vista del logbook pre-rellenado + formulario de campos faltantes + firma |
| **Configuración de integración** | Connect | Conexión con cuenta DJI FlightHub 2 del operador |
| **Perfil de piloto** | Personal (básico) | Datos del piloto, licencias, historial de vuelos |

---

## 5. Infraestructura y Servidores

### Cloud Provider

| Opción | Prioridad | Razón |
|---|---|---|
| **AWS** | Primera opción | Mayor créditos startup (AWS Activate: $100K+), mejor ecosistema en Europa |
| **Azure** | Alternativa | Preferible si se apunta a clientes enterprise Microsoft |
| **Hetzner Cloud** | Opción low-cost MVP | Datacenter en Europa (GDPR), 10x más barato para bootstrapping |

### Arquitectura de despliegue

```
Producción:
├─ Kubernetes (EKS / AKS) o Docker Compose (MVP simplificado)
├─ CI/CD: GitHub Actions → ECR → EKS
├─ CDN: CloudFront (AWS) para assets del frontend
├─ DNS: Route53 + certificados SSL automáticos (ACM)
└─ Backups: automatizados diarios + point-in-time recovery (PostgreSQL)

Región principal: eu-west-1 (Irlanda) o eu-central-1 (Frankfurt)
→ GDPR compliance + baja latencia para clientes europeos
```

### Escalabilidad

- MVP: Docker Compose en una VPS / instancia EC2 small (~€50-150/mes)
- Fase 2: Kubernetes con autoscaling (€300-800/mes)
- Fase 3: Multi-region, disaster recovery, SLA 99.9%

---

## 6. Ciberseguridad

Ver [[conceptos/zero-trust-architecture]] para el framework completo.

### Requisitos de seguridad no negociables (MVP)

| Requisito | Implementación |
|---|---|
| Autenticación robusta | OAuth 2.0 + PKCE + MFA opcional |
| Cifrado en tránsito | TLS 1.3 obligatorio en todas las conexiones |
| Cifrado en reposo | AES-256 para datos sensibles (datos de pilotos, rutas de vuelo) |
| Aislamiento de tenants | Row-Level Security en PostgreSQL por organización |
| Logs de auditoría | Registro inmutable de todas las acciones sobre logbooks |
| GDPR | Derecho de exportación y borrado de datos de usuario |
| Firma de logbooks | Hash SHA-256 del contenido al momento de firma → detecta alteraciones |

### Amenazas específicas UAS a mitigar

- GPS Spoofing: validación de coherencia de coordenadas (velocidad, altitud)
- Manipulación de logbooks: hash + firma digital del piloto
- Exfiltración de rutas: datos de vuelo cifrados + acceso por rol

---

## 7. Gráficos y Visualización de Datos

| Tipo de visualización | Herramienta | Módulo |
|---|---|---|
| Trayectoria de vuelo en mapa | Mapbox GL JS | Logbook, Missions |
| Gráfico de altitud/velocidad vs. tiempo | Recharts | Logbook detalle |
| Estado de flota (semáforo) | Custom SVG + CSS | Dashboard |
| Calendario de operaciones | Custom o FullCalendar | Missions |
| Gráfico de horas de vuelo acumuladas | Recharts | Personal, Dashboard |
| Alertas de mantenimiento | Lista + indicadores de urgencia | Fleet |

---

## 8. Requisitos No Funcionales

| Requisito | Valor objetivo |
|---|---|
| Disponibilidad | 99.5% (MVP) → 99.9% (Fase 2) |
| Latencia API (p95) | <300ms |
| Tiempo de carga initial (web) | <2s |
| Soporte de navegadores | Chrome, Firefox, Safari, Edge (últimas 2 versiones) |
| Mobile responsive | Obligatorio desde el MVP |
| Idiomas | Español + Inglés desde el lanzamiento |
| Cumplimiento GDPR | Obligatorio antes de lanzamiento público |

---

## 9. Roadmap Técnico Sugerido

| Hito | Duración estimada | Entregable |
|---|---|---|
| **PoC FlightHub API** | 1-2 semanas | Script que extrae vuelo y genera logbook borrador |
| **MVP backend** | 6-10 semanas | Logbook Service + Fleet Service + Auth |
| **MVP frontend** | 4-6 semanas | Dashboard + Logbook + Firma |
| **Integración FlightHub completa** | 3-4 semanas | Flujo end-to-end automático |
| **Beta privada** | 4 semanas | 5-10 clientes beta, feedback loop |
| **Lanzamiento v1.0** | 2 semanas | Producción, onboarding documentado |

---

## Fuentes citadas

- [[fuentes/esquema-inicial-whiteboard]]
