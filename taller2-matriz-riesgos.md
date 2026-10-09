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
*   **Vulnerabilidad:** El análisis forense no ha establecido si hubo descuido o entrega deliberada de una credencial de alto privilegio, lo que sugiere que el control sobre estas credenciales es limitado [(La FM, 2026; La República, 2026)].
*   **Riesgo:** Un atacante con credenciales de alto privilegio podría comprometer el dominio completo y desplegar ransomware en minutos, como hace “The Gentlemen” [(El Espectador, 2026)].
*   **Probabilidad:** 3. No confirmado, pero es la hipótesis principal de la investigación forense.
*   **Impacto:** 5. Una credencial de dominio comprometida puede cifrar toda la infraestructura.
*   **Nivel:** 15.
*   **Control actual o evidencia:** Sin evidencia pública de gestión de credenciales privilegiadas (PAM) ni rotación de estas.
*   **Control propuesto:** Implementar gestión de accesos privilegiados (PAM), rotación automática de credenciales de administrador y autenticación sin contraseña para cuentas de alto privilegio.
*   **Justificación:** El actor “The Gentlemen” tiene capacidad demostrada de comprometer dominios completos con credenciales de administrador.
*   **Marco relacionado:** ISO/IEC 27001 y COBIT (gestión de identidades y accesos privilegiados).

### R-04 — Respaldos e integridad de la información
*   **Activo o proceso:** Copias de seguridad, respaldos de información corporativa y mecanismos de recuperación de datos.
*   **Amenaza:** Ataque de ransomware que pueda cifrar, modificar o eliminar información, así como comprometer las copias de seguridad.
*   **Vulnerabilidad:** Posible falta de protección y aislamiento de las copias de seguridad.
*   **Riesgo:** Un atacante podría comprometer los respaldos y alterar o eliminar información importante, dificultando la recuperación de los sistemas después de un ataque y aumentando el tiempo de indisponibilidad de los servicios.
*   **Probabilidad:** 3. Ya ocurrió un acceso no autorizado a la nube, aunque no se confirmó que los respaldos fueran afectados.
*   **Impacto:** 5. La pérdida o alteración de las copias de seguridad podría dificultar la recuperación de información crítica y generar consecuencias operativas y económicas.
*   **Nivel:** 15.
*   **Control actual o evidencia:** Ecopetrol tomó medidas para controlar el incidente, pero no se conoce públicamente cómo están protegidos todos sus respaldos.
*   **Control propuesto:** Crear copias de seguridad protegidas, mantenerlas separadas de los sistemas principales y probar periódicamente su recuperación.
*   **Justificación:** Los respaldos constituyen una medida esencial para recuperar la información después de un ataque. Si también son comprometidos, la organización puede perder una de sus principales herramientas de recuperación.
*   **Marco relacionado:** ISO 27001, porque ayuda a proteger la información y mantener su disponibilidad.

### R-05 — Información financiera y operativa descargada
*   **Activo o proceso:** Información financiera, administrativa y operativa de Ecopetrol.
*   **Amenaza:** Robo y publicación de información confidencial.
*   **Vulnerabilidad:** Posibles debilidades en la clasificación de la información, los permisos de acceso, el monitoreo de descargas y los mecanismos de prevención de fuga de datos.
*   **Riesgo:** La publicación de información financiera u operativa podría exponer datos confidenciales, facilitar nuevos ataques, afectar la confianza de las partes interesadas y generar consecuencias legales o reputacionales para Ecopetrol y sus compañías relacionadas.
*   **Probabilidad:** 4. La información fue extraída y posteriormente se publicaron archivos.
*   **Impacto:** 3. La filtración podría generar pérdidas económicas indirectas y afectar la confianza en la empresa.
*   **Nivel:** 12.
*   **Control actual o evidencia:** se revocaron accesos y se adoptaron medidas de contención. La publicación posterior de archivos en la demuestra que parte de la información extraída quedó expuesta. No se dispone de información pública suficiente para determinar el alcance de todos los controles de prevención de fuga de datos.
*   **Control propuesto:** Limitar el acceso a los archivos, proteger los datos importantes y utilizar herramientas que detecten posibles filtraciones.
*   **Justificación:** La confidencialidad de la información es fundamental para proteger los procesos internos y la reputación de la organización. Aunque el incidente no haya generado una interrupción operativa ni un impacto financiero directo, la divulgación de documentos puede producir consecuencias posteriores.
*   **Marco relacionado:** ISO 27001, porque se enfoca en la seguridad y confidencialidad de la información.

### R-06 — Infraestructura OT (SCADA)
*   **Activo o proceso:** Sistemas SCADA utilizados para supervisar y controlar procesos industriales de Ecopetrol.
*   **Amenaza:** Acceso no autorizado de actores externos, propagación de ransomware desde redes corporativas hacia redes industriales o manipulación de sistemas de control.
*   **Vulnerabilidad:** Posibles fallas en la separación entre las redes corporativas y las redes industriales.
*   **Riesgo:** Un atacante podría afectar los procesos industriales y ocasionar interrupciones en las operaciones.
*   **Probabilidad:** 3. Hubo un incidente de ciberseguridad, pero no se confirmó que los sistemas SCADA fueran afectados.
*   **Impacto:** 4. Una afectación a la infraestructura industrial podría ocasionar interrupciones operativas, daños en equipos y riesgos para las personas y el medioambiente.
*   **Nivel:** 12.
*   **Control actual o evidencia:** De acuerdo con caso, no hubo interrupción operativa. Sin embargo, esto no permite confirmar por sí solo el estado de la segmentación de redes OT, los controles de acceso remoto o los mecanismos de detección industrial.
*   **Control propuesto:** Separar las redes corporativas de las redes OT mediante segmentación y zonas de seguridad, controlar estrictamente los accesos remotos, utilizar listas de autorización, monitorear el tráfico industrial y establecer procedimientos de recuperación específicos para los sistemas SCADA.
*   **Justificación:** Los sistemas industriales requieren medidas de protección especializadas porque una afectación puede tener consecuencias que van más allá de la pérdida de información, comprometiendo la continuidad de los procesos y la seguridad de las instalaciones.
*   **Marco relacionado:** ISO/IEC 27001 (gestión de riesgos y controles de seguridad), COBIT (gobierno y gestión de TI) e ITIL (gestión de incidentes, continuidad y disponibilidad de los servicios).

### Conclusión

Con el desarrollo del taller se pudieron identificar los principales riesgos de ciberseguridad relacionados con el incidente de Ecopetrol, como el acceso a la nube, las cuentas de usuario, las credenciales, los respaldos, la filtración de información y los sistemas industriales.

Los riesgos más altos fueron el almacenamiento en la nube y las cuentas corporativas, con un nivel de 16. Esto da a entender la importancia de mejorar los controles de acceso, utilizar autenticaciones y vigilar las descargas de información.

También se pudo entender cómo ISO 27001, COBIT e ITIL ayudan a mejorar la seguridad, controlar los riesgos y responder ante incidentes. En conclusión, el caso demuestra que no basta con detener un ataque, sino que también es necesario proteger la información, evitar nuevas filtraciones y estar preparados para recuperar los sistemas si ocurre otro incidente.
