---
title: "Imagen de Marca y Valores — U-Log"
date: 2026-05-08
query_origin: "Definición de identidad visual y valores de marca para U-Log"
tags: [marca, identidad-visual, valores, ux, diseno, dark-cockpit]
fuentes_citadas: [esquema-inicial-whiteboard]
---

# Imagen de Marca y Valores — U-Log

## Reencuadre estratégico de la marca

U-Log no es "otra app de gestión de drones". Es **infraestructura operacional crítica para activos aéreos autónomos**.

El cambio de lenguaje es intencionado:

| Lenguaje que evitar | Lenguaje de marca U-Log |
|---|---|
| "gestión de drones" | "Autonomous Aerial Asset Management" |
| "software para pilotos" | "Plataforma operacional UAS certificada" |
| "diario de vuelo digital" | "Logbook de trazabilidad EASA" |
| "app de mantenimiento" | "Sistema de gestión de ciclo de vida de activos" |

---

## 1. Valores de Marca

| Valor | Significado operacional | Manifestación en producto |
|---|---|---|
| **Precisión** | Datos exactos, sin ambigüedad ni error humano | Logbooks desde telemetría real, no entrada manual |
| **Confianza** | Reguladores y clientes confían en los datos | Integridad criptográfica de registros, formato EASA |
| **Soberanía** | El operador es dueño de sus datos | Arquitectura cloud con exportación libre, sin lock-in |
| **Escalabilidad** | La plataforma crece con la flota | Multi-flota, multi-organización, API-first |
| **Fluidez** | Cero fricción operacional | Workflows de un clic, notificaciones proactivas |
| **Seguridad** | Datos y operaciones protegidos | Zero Trust, cifrado E2E, logs inmutables |

---

## 2. Filosofía de Diseño: Dark Cockpit

Inspirado en la filosofía de cabina aeronáutica profesional: **bajo ruido cognitivo, máxima densidad de información crítica, cero decoración superflua**.

### Principios

1. **Silencio visual por defecto** — la pantalla no habla si no hay nada que reportar
2. **Semáforo de estado** — verde / ámbar / rojo para estado de flota, personal y cumplimiento
3. **Datos sobre decoración** — cada elemento visual tiene función operacional
4. **Consistencia total** — el operador no piensa dónde está la información, la conoce

### Tipografía

| Uso | Fuente | Razón |
|---|---|---|
| Interfaz principal | **Inter** (o Helvetica Neue) | Institucional, legible en pantallas de control |
| Datos técnicos, IDs, coordenadas | **JetBrains Mono** | Claridad en strings técnicos |
| Marketing / landing page | Inter + peso semibold | Consistencia de marca |

Escala tipográfica reducida: máximo 4 tamaños (12 / 14 / 16 / 24px) para consistencia total.

### Paleta de Color

| Rol | Nombre | Hex |
|---|---|---|
| Fondo principal | Negro aeronáutico | `#0D1117` |
| Fondo secundario / cards | Carbono | `#161B22` |
| Bordes y separadores | Gris estructural | `#21262D` |
| Texto principal | Blanco nieve | `#F0F6FC` |
| Texto secundario | Gris claro | `#8B949E` |
| Estado: operativo / OK | Verde pista | `#3FB950` |
| Estado: atención / alerta | Ámbar | `#D29922` |
| Estado: crítico / error | Rojo emergencia | `#F85149` |
| Acento primario / CTAs | Azul eléctrico | `#58A6FF` |
| Acento secundario | Índigo institucional | `#6E76E5` |

### Iconografía

- Sistema base: **Lucide Icons** (outline) — limpio, consistente, open source
- Iconos UAS específicos: custom design basado en simbología ICAO simplificada
- Regla: sin emojis en contexto operacional — solo admitidos en onboarding y marketing

---

## 3. Personalidad y Tono de Voz

| Atributo | Descripción |
|---|---|
| **Tono** | Técnico, directo, sin condescendencia |
| **Formalidad** | Profesional (no corporativo frío, no startup informal) |
| **Metáfora central** | "Torre de control para tu flota" |
| **Anti-patrones** | Sin gamificación, sin lenguaje "friendly startup", sin exclamaciones |

### Ejemplos de tono correcto vs. incorrecto

| Incorrecto | Correcto |
|---|---|
| "¡Hey! 🚀 3 drones listos para volar hoy! 🎉" | "3 aeronaves operativas. 1 en mantenimiento programado." |
| "¡Hemos rellenado tu diario de vuelo! Échale un vistazo 😊" | "Logbook generado automáticamente. Revisa y firma." |
| "¡Genial, has completado tu primer vuelo!" | "Vuelo registrado. Logbook pendiente de firma." |

---

## 4. Naming de Módulos

| Módulo interno | Nombre UI propuesto | Lógica de naming |
|---|---|---|
| PROP DRON | **Fleet** | Activos de la organización |
| CHECK | **Ops** | Operaciones diarias, checklists |
| OPERACIONES | **Missions** | Misiones planificadas y ejecutadas |
| HUB / NODO | **Connect** | Integraciones y conectividad |
| LOG | **Logbook** | Registro oficial — nombre ya estándar en el sector |
| DOCK | **Docs** | Documentación y cumplimiento |

---

## 5. Activos de Marca a Desarrollar

### Identidad visual (alta prioridad)

- [ ] **Logotipo** — concepto: "U" con trayectoria de vuelo integrada; wordmark + símbolo separables
- [ ] **Sistema de iconos de módulos** — set personalizado basado en Lucide
- [ ] **Mockups de pantallas clave**: Dashboard operacional, vista Logbook, Fleet overview
- [ ] **Brand guidelines PDF** — para proveedores, inversores y futuros diseñadores

### Activos digitales (media prioridad)

- [ ] Landing page con identidad Dark Cockpit
- [ ] Ilustraciones para estados vacíos (empty states) y onboarding
- [ ] Plantillas de presentación para inversores / demos
- [ ] Favicon y app icon (símbolo de la U)

---

## Fuentes citadas

- [[fuentes/esquema-inicial-whiteboard]]
