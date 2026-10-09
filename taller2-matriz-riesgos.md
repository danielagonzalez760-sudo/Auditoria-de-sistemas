# Matriz inicial de riesgos

**Auditoría de Sistemas (ET0114) · Sesión 7 · Matriz de análisis de riesgos**
**Docente:** Juan Duque
**Fecha de entrega:** viernes 9 de octubre de 2026

**Integrantes del grupo:**
*   Daniela Gonzalez Tarraz
*   Juan David Lopez

## Caso y contexto actualizado

Seguimos con **Ecopetrol**. Para esta entrega nos enfocamos en el incidente de ciberseguridad del 17 de julio de 2026, cuando un actor externo accedió a entornos de almacenamiento en la nube de aproximadamente 15 compañías del Grupo Empresarial, descargó información de 3.300 cuentas de usuario e intentó ejecutar un ransomware que fue bloqueado. Aunque no hubo interrupción operativa ni impacto financiero directo, los atacantes publicaron posteriormente los archivos en la dark web, y algunos fueron clasificados como críticos [(Reuters, 2026; El Espectador, 2026)]. Los marcos del primer taller (ISO 27001, COBIT e ITIL) siguen siendo la referencia para decidir qué controles esperar.

## Resumen de riesgos

| ID | Activo o proceso | Nivel | Prioridad |
|---|---|---:|---|
| R-01 | Almacenamiento en la nube del Grupo | 16 | Alta |
| R-02 | Cuentas de usuario corporativas | 16 | Alta |
| R-03 | Credenciales con privilegios elevados | 15 | Alta |
| R-04 | Respaldos e integridad de información | 15 | Alta |
| R-05 | Información financiera y operativa descargada | 12 | Media |
| R-06 | Infraestructura OT (SCADA) | 12 | Media |

---

## Matriz detallada

### R-01 — Almacenamiento en la nube del Grupo Empresarial
*   **Activo o proceso:** Entornos de almacenamiento en la nube de aproximadamente 15 compañías del Grupo Ecopetrol.
*   **Amenaza:** Grupo de ransomware “The Gentlemen”, especializado en doble extorsión.
*   **Vulnerabilidad:** Los entornos de almacenamiento en la nube no contaban con controles suficientes para impedir la descarga masiva de archivos por parte de un actor externo.
*   **Riesgo:** El actor externo podría descargar información sensible de múltiples compañías del Grupo porque los controles de descarga masiva no bloquearon el acceso inicial, como efectivamente ocurrió con 3.300 cuentas comprometidas [(Reuters, 2026; El Espectador, 2026)].
*   **Probabilidad:** 4. La amenaza se materializó el 17 de julio de 2026 y el actor ya demostró capacidad de acceso.
*   **Impacto:** 4. Afectó a 15 compañías del Grupo, expuso información corporativa y generó extorsión.
*   **Nivel:** 16.
*   **Control actual o evidencia:** Ecopetrol bloqueó el ransomware y revocó accesos, pero la descarga masiva ya había ocurrido [(Comunicado oficial Ecopetrol, 2026)].
*   **Control propuesto:** Restringir descargas masivas desde cuentas individuales, implementar alertas automáticas ante volúmenes anómalos de descarga y segmentar los entornos de almacenamiento por compañía.
*   **Justificación:** Es el riesgo de mayor nivel porque el incidente demostró que el control de descarga masiva no fue suficiente para prevenir la extracción.
*   **Marco relacionado:** ISO/IEC 27001 (control de acceso y protección de datos).

### R-02 — Cuentas de usuario corporativas
*   **Activo o proceso:** Cuentas de usuario de 15 compañías del Grupo (3.300 cuentas afectadas).
*   **Amenaza:** Atacante externo con acceso a credenciales o sesiones activas.
*   **Vulnerabilidad:** Las cuentas comprometidas permitieron la descarga de información asociada sin que se activara un segundo factor de autenticación para operaciones sensibles.
*   **Riesgo:** Un atacante podría acceder nuevamente a cuentas corporativas porque no se ha confirmado que el MFA sea obligatorio para todas las cuentas y operaciones de descarga, exponiendo información sensible [(La FM, 2026; La República, 2026)].
*   **Probabilidad:** 4. El atacante ya accedió a miles de cuentas; el vector sigue siendo viable si no se refuerza.
*   **Impacto:** 4. Expone información corporativa y personal, con riesgo reputacional.
*   **Nivel:** 16.
*   **Control actual o evidencia:** Ecopetrol revocó accesos comprometidos y bloqueó mecanismos de descarga masiva [(Comunicado oficial de Ecopetrol, 2026)]. No hay evidencia pública de MFA obligatorio general.
*   **Control propuesto:** MFA obligatorio para el 100% de las cuentas, especialmente para operaciones de descarga y acceso a almacenamiento en la nube; monitoreo de inicios de sesión anómalos.
*   **Justificación:** El número de cuentas afectadas (3.300) demuestra que el control de acceso basado solo en credenciales es insuficiente.emuestra que el control de acceso basado solo en credenciales es insuficiente.
*   **Marco relacionado:** ISO/IEC 27001 (control de acceso).

*   ### R-03 — Credenciales con privilegios elevados
*   **Activo o proceso:** Credenciales de administrador o con privilegios sobre servicios en la nube.
*   **Amenaza:** Uso indebido de una credencial con altos privilegios (hipótesis investigada por las autoridades).
*   **Vulnerabilidad:** El análisis forense no ha establecido si hubo descuido o entrega deliberada de una credencial de alto privilegio, lo que sugiere que el control sobre estas credenciales es limitado [citation:7].
*   **Riesgo:** Un atacante con credenciales de alto privilegio podría comprometer el dominio completo y desplegar ransomware en minutos, como hace “The Gentlemen” [(El Espectador, 2026)].
*   **Probabilidad:** 3. No confirmado, pero es la hipótesis principal de la investigación forense.
*   **Impacto:** 5. Una credencial de dominio comprometida puede cifrar toda la infraestructura.
*   **Nivel:** 15.
*   **Control actual o evidencia:** Sin evidencia pública de gestión de credenciales privilegiadas (PAM) ni rotación de estas.
*   **Control propuesto:** Implementar gestión de accesos privilegiados (PAM), rotación automática de credenciales de administrador y autenticación sin contraseña para cuentas de alto privilegio.
*   **Justificación:** El actor “The Gentlemen” tiene capacidad demostrada de comprometer dominios completos con credenciales de administrador.
*   **Marco relacionado:** ISO/IEC 27001 y COBIT (gestión de identidades y accesos privilegiados).
