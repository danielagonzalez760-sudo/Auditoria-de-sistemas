# Informe de auditoría y plan de acción

**Auditoría de Sistemas (ET0114) · Taller final**
**Docente:** Juan Duque
**Presentación:** viernes 27 de noviembre de 2026
**Entrega del informe:** domingo 29 de noviembre de 2026

**Integrantes del grupo:**
* Daniela Gonzalez Tarraz
* Juan David Lopez

> ⚠️ **Aviso de ejercicio simulado.** El contexto del caso (el ciberataque a Ecopetrol de julio de 2026) es real y está respaldado por fuentes públicas. **La política evaluada, la población, la muestra y los resultados de la prueba son ficticios**, creados para este taller. No tuvimos acceso a sistemas ni registros de Ecopetrol. Ninguna conclusión de este informe describe el estado real de los controles de la empresa.

---
## 1. Identificación y resumen ejecutivo

| Campo | Detalle |
|---|---|
| **Organización** | Ecopetrol S.A. y compañías de su Grupo Empresarial |
| **Riesgo evaluado** | R-01 y R-02 de la matriz: acceso y descarga masiva de información en el almacenamiento en la nube (nivel 16) |
| **Control probado** | Alerta y bloqueo automático de descargas masivas en el almacenamiento en la nube |
| **Tipo de ejercicio** | Simulado (datos ficticios claramente identificados) |
| **Resultado principal** | En la muestra simulada, 7 sesiones superaron el umbral. El control operó como se esperaba en 5 de ellas; se registraron **2 excepciones**: una sesión sin alerta y una alerta fuera del plazo |

**Resumen.** El 17 de julio de 2026, Ecopetrol informó un acceso no autorizado a entornos de almacenamiento de archivos en la nube de aproximadamente 15 compañías del Grupo, con la descarga de datos asociados a unas 3.300 cuentas de usuario (El País, 2026). Los controles de la empresa bloquearon el intento de cifrado (ransomware), pero no evitaron la extracción de archivos (ITSitio, 2026). Por eso, en nuestra matriz de riesgos este escenario quedó con el nivel más alto, y en el plan de auditoría definimos cómo verificar el control que debía detener la extracción.

En este taller ejecutamos, con datos simulados, el **procedimiento de operación** del plan: comparar sesiones de descarga contra el umbral de una política ficticia y verificar si el sistema generó la alerta y el bloqueo esperados. En 2 de las 7 sesiones simuladas que superaron el umbral, el control no operó como lo exige la política simulada. La causa no quedó establecida con la prueba.
