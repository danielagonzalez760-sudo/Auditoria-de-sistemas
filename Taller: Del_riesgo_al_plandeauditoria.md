# Plan de Auditoría: Control de acceso y descargas en la nube

**Auditoría de Sistemas (ET0114) · Taller: del riesgo priorizado al plan de auditoría**
**Docente:** Juan Duque
**Exposición:** viernes 30 de octubre de 2026
**Fecha de entrega:** domingo 1 de noviembre de 2026

**Integrantes del grupo:**
*   Daniela Gonzalez Tarraz
*   Juan David Lopez

**Enlace matriz de riesgos:** [https://github.com/danielagonzalez760-sudo/Auditoria-de-sistemas/blob/main/taller2-matriz-riesgos.md]

---

## 1. Contexto y riesgo seleccionado

**Organización:** Ecopetrol S.A.
**Contexto:** Tras el ciberataque de julio de 2026, donde un actor externo accedió a entornos en la nube de 15 compañías del Grupo y descargó información de 3.300 cuentas, la preocupación central sigue siendo la protección de la información y la contención de nuevos accesos no autorizados.

**Riesgos seleccionados (R-01 y R-02 de la matriz):**
*   **Activos:** Entornos de almacenamiento en la nube y cuentas de usuario corporativas.
*   **Amenaza:** Grupo de ransomware “The Gentlemen” (actores con acceso a credenciales).
*   **Vulnerabilidad:** Los controles de descarga masiva no bloquearon la extracción, y no se ha confirmado que el MFA sea obligatorio para todas las cuentas.
*   **Consecuencia:** Exposición de información sensible (3.300 cuentas) y extorsión.
*   **Nivel de riesgo:** 16 para ambos (Probabilidad 4 × Impacto 4).

**¿Por qué le dedicamos una auditoría?**
El incidente real demostró que la vulnerabilidad es demasiado riesgosa. El proceso de gestión de identidades y el control de descargas en la nube son la primera línea de defensa de Ecopetrol. Auditar esto nos permitirá saber si las medidas de contención aplicadas tras el ataque (revocar accesos) fueron un parche temporal o si el diseño del control de acceso realmente se reforzó.
---

## 2. Objetivo de auditoría

**Objetivo principal:**
> *Determinar si los controles de autenticación (MFA) y restricción de descargas masivas en los entornos de almacenamiento en la nube del Grupo Ecopetrol operaron de manera efectiva durante el periodo del 1 de julio al 30 de septiembre de 2026, de acuerdo con las políticas de seguridad de la información vigentes.*

---

## 3. Alcance funcional

1.  **Proceso o función:** Gestión de identidades, autenticación y control de descargas en la nube.
2.  **Sistema o componente:** Plataformas de almacenamiento en la nube (ej. Microsoft 365, Google Workspace o AWS) y el directorio activo corporativo.
3.  **Población:** Registros de logs (inicios de sesión, descargas) y las cuentas de usuario con acceso a los repositorios de archivos del Grupo.
4.  **Periodo:** 1 de julio al 30 de septiembre de 2026 (abarca el mes del ataque y los dos meses posteriores, donde debieron implementarse las correcciones).
5.  **Áreas o responsables:** Dirección de Ciberseguridad, Equipo de Infraestructura Cloud y Auditoría Interna.
6.  **Inclusiones:** Logs de eventos de seguridad de la nube, políticas de control de acceso, configuraciones de MFA y alertas de descargas anómalas.
7.  **Exclusiones:** No se auditará la infraestructura física (servidores on-premise) ni los sistemas OT/SCADA (R-06), ya que este plan se concentra puramente en el entorno cloud. *Esta exclusión limita la conclusión únicamente al acceso a la nube.*

---

## 4. Criterios de evaluación

Evaluaremos el control basándonos en el estándar **ISO/IEC 27001** y lo que debería estar en la política interna de la empresa.

| Control a evaluar | Criterio de evaluación (Condición esperada) | Fuente del criterio |
|---|---|---|
| **Autenticación (MFA)** | El acceso a las plataformas de nube y las operaciones de descarga deben requerir obligatoriamente un segundo factor de autenticación. | ISO/IEC 27001 (Control A.5.17) y política interna de seguridad. |
| **Restricción de descargas** | El sistema debe bloquear o alertar sobre descargas de archivos que superen un umbral determinado por usuario en un tiempo específico. | Procedimiento interno de gestión de accesos e ISO/IEC 27001 (A.8.12). *Criterio por confirmar mediante solicitud de la política.* |
| **Monitoreo y alertas** | Los intentos de acceso fallidos reiterados o descargas inusuales deben generar alertas al equipo de seguridad. | Política de gestión de incidentes (soporte de ITIL). *Umbral de tiempo por confirmar.* |

---

## 5. Programa de trabajo (Procedimientos)

Diseñamos dos procedimientos complementarios para cubrir el diseño y la operación del control.

### Procedimiento 1: Verificación del diseño (¿Cómo debería funcionar?)
* **Control:** Configuración de MFA y bloqueo de descargas.
* **Qué haremos:** Entrevistaremos al líder de Ciberseguridad y revisaremos la configuración del directorio activo y del tenant en la nube.
* **Población:** Configuración global del directorio y de la plataforma cloud.
* **Evidencia esperada:** Capturas de pantalla de la configuración de MFA (demostrando que está forzado) y el documento del procedimiento de gestión de accesos.
* **Posibles excepciones:** Encontrar cuentas de servicio o "break glass" (emergencia) sin MFA habilitado.

### Procedimiento 2: Prueba de operación (¿Realmente funcionó?)
* **Control:** Eficacia del monitoreo de descargas masivas.
* **Qué haremos:** Extraeremos los logs de auditoría de la plataforma cloud (eventos de descarga) y filtraremos los volúmenes anómalos.
* **Población o muestra:** Revisaremos una muestra de los logs de descargas del periodo. Propondremos tomar el 10% de los eventos más grandes o, de ser posible, los logs de las 3.300 cuentas afectadas.
* **Qué compararemos:** La cantidad de archivos descargados contra el umbral definido. ¿El sistema emitió alertas? ¿Bloqueó la descarga?
* **Evidencia esperada:** Archivos CSV con los logs, capturas del panel de alertas (SIEM) y tickets de incidentes generados.
* **Posibles excepciones:** Encontrar en los logs que una cuenta descargó cientos de archivos y el sistema no generó ninguna alerta.

---

## 6. Organización de la ejecución (Cronograma y responsables)

*Planificación propuesta. La ejecución real depende del acceso que brinde Ecopetrol.*

| Fase | Actividad | Responsable | Tiempo estimado |
|---|---|---|---|
| **Preparación** | Solicitud formal de políticas y creación de la muestra. | Daniela Gonzalez | 3 días |
| **Ejecución 1** | Entrevista con Ciberseguridad y revisión de configuraciones (Diseño). | Juan David Lopez | 2 días |
| **Ejecución 2** | Extracción y análisis de logs en la nube (Operación). | Ambos auditores | 5 días |
| **Cierre** | Redacción de hallazgos y socialización. | Ambos auditores | 3 días |

**Dependencias:** Necesitamos que TI de Ecopetrol nos dé acceso de solo lectura a los logs y nos confirme el procedimiento interno de retención de datos.

---

## 7. Supuestos y limitaciones

* **Hechos comprobados (según la matriz):** Ocurrió el ataque el 17 de julio de 2026, se descargaron 3.300 cuentas, el ransomware fue bloqueado y se revocaron accesos.
* **Supuestos:** Asumimos que la empresa cuenta con herramientas de monitoreo (SIEM) y que las políticas están documentadas. Asumimos que las descargas se hacen a través de la nube y no por canales alternos.
* **Información por solicitar:** Políticas de control de acceso, procedimiento de gestión de descargas y los logs reales de la plataforma.
* **Limitaciones:** Al ser un plan de auditoría para el taller, no tenemos acceso a los logs reales. Si TI no tiene activadas las alertas, nuestra prueba arrojaría una excepción por falta de evidencia.

---

## 8. Fila de trazabilidad (Resumen)

| ID del riesgo | Control a evaluar | Criterio y fuente | Procedimiento | Población o muestra | Evidencia esperada |
|---|---|---|---|---|---|
| **R-01 y R-02** | MFA y bloqueo de descargas masivas | ISO 27001 (A.5.17 y A.8.12) / Política Interna | 1. Revisión de configuración (Diseño).<br>2. Análisis de logs (Operación). | Configuración del tenant y logs del 1 de julio al 30 de septiembre de 2026. | Capturas de configuración, CSV de logs, tickets de alertas. |
