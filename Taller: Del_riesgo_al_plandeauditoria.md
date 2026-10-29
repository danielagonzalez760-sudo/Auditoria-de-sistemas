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

