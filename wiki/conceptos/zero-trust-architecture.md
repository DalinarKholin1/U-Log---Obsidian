---
title: "Zero Trust Architecture"
tags: [ciberseguridad, zero-trust, arquitectura, telemetria-uas, mision-critica]
source_count: 1
---

# Zero Trust Architecture

## Definición

Modelo de seguridad informática donde **ningún usuario, dispositivo o sistema es confiable por defecto**, independientemente de si está dentro o fuera del perímetro de red corporativa. Toda solicitud de acceso se autentica, autoriza y registra de forma continua. Es el estándar recomendado para sistemas que gestionan datos operacionales críticos de aviación.

## Aplicación a U-Log

| Principio ZTA                 | Implementación en U-Log                                                 |
| ----------------------------- | ----------------------------------------------------------------------- |
| **Verificar explícitamente**  | OAuth 2.0 + MFA obligatorio para todos los accesos                      |
| **Mínimo privilegio**         | RBAC granular: piloto / técnico MTX / manager / auditor / admin         |
| **Asumir brecha**             | Cifrado AES-256 en reposo + TLS 1.3 en tránsito para toda la telemetría |
| **Microsegmentación**         | mTLS entre microservicios internos                                      |
| **Monitorización continua**   | Logs de auditoría inmutables + alertas de anomalías                     |
| **Identidad del dispositivo** | Certificados de dispositivo para integraciones hardware (drones, GCS)   |

## Amenazas específicas del contexto UAS

| Amenaza                          | Descripción                                         | Mitigación en U-Log                                            |
| -------------------------------- | --------------------------------------------------- | -------------------------------------------------------------- |
| **GPS Spoofing**                 | Falsificación de coordenadas de vuelo               | Validación cruzada de telemetría + firma hash de datos         |
| **Signal Jamming**               | Interrupción del enlace C2                          | Diseño tolerante a fallos; U-Log registra el gap, no lo oculta |
| **Acceso no autorizado a datos** | Exfiltración de rutas de vuelo / datos de clientes  | ZTA + cifrado por tenant                                       |
| **Manipulación de logbooks**     | Alteración de registros para evitar responsabilidad | Logbooks firmados digitalmente + hash inmutable                |
| **API compromise**               | Ataque a la integración FlightHub                   | API keys rotativas + rate limiting + IP allowlist              |

## Relevancia para el mercado enterprise / B2G

Los clientes enterprise (inspección de infraestructuras críticas, seguridad pública) y B2G (administraciones) exigen explícitamente:
- Certificación ISO 27001 (objetivo a medio plazo)
- Cumplimiento ENS (Esquema Nacional de Seguridad) para contratos públicos españoles
- GDPR para datos de pilotos y operaciones

## Fuentes que lo mencionan

- [[fuentes/esquema-inicial-whiteboard]] — "Seguridad" como valor de producto y requisito técnico

## Perspectivas distintas

- **Operador PYME**: quiere seguridad pero sin complejidad de configuración → ZTA debe ser transparente
- **Cliente enterprise**: exige auditoría, certificaciones y SLAs de disponibilidad
- **Regulador**: requiere integridad e inmutabilidad de los registros de vuelo

## Contradicciones detectadas

Ninguna aún.
