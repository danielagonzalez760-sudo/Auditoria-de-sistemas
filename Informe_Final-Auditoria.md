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

## 2. Objetivo y alcance

**Objetivo (tomado del plan de auditoría):**
> Determinar si el control de alerta y bloqueo de descargas masivas en los entornos de almacenamiento en la nube operó de manera efectiva entre el 1 de julio y el 30 de septiembre de 2026, de acuerdo con la política de seguridad aplicable.

| Elemento | Definición |
|---|---|
| **Proceso** | Monitoreo y control de descargas en el almacenamiento en la nube |
| **Sistema** | Plataforma de almacenamiento en la nube corporativa y su herramienta de monitoreo de seguridad (SIEM) |
| **Periodo** | 1 de julio al 30 de septiembre de 2026 |
| **Población (simulada)** | 1.240 sesiones de descarga registradas en el periodo |
| **Muestra (simulada)** | 10 sesiones (ver sección 3) |
| **Exclusiones** | Sistemas SCADA y red OT (riesgo R-06), servidores físicos on-premise y el procedimiento de diseño del plan (revisión de configuración de MFA), que no se ejecutó en este taller. La conclusión aplica solo al control de descargas en la nube y a la muestra revisada |

---

## 3. Criterios y metodología

### 3.1 Criterio

| Elemento | Detalle |
|---|---|
| **Criterio (política ficticia)** | *Política simulada PS-CIB-07:* toda sesión que descargue **más de 100 archivos en 60 minutos** debe generar una **alerta en el SIEM en máximo 15 minutos** y la sesión debe quedar **bloqueada** |
| **Fuente** | Regla ficticia creada para el taller. Se alinea con ISO/IEC 27001:2022, controles **A.8.12** (prevención de fuga de datos) y **A.8.16** (actividades de monitoreo) |
| **Responsable del control (supuesto)** | Equipo de monitoreo de seguridad (SOC) de la Dirección de Ciberseguridad |

### 3.2 Selección de la muestra

Seleccionamos las **10 sesiones con mayor volumen de descarga** del periodo (selección dirigida o por juicio). Elegimos este método porque el riesgo que auditamos es la descarga masiva: las sesiones más grandes son justamente donde el control debía activarse. Incluir las sesiones cercanas al umbral también permite comprobar que el sistema no alerta por debajo de él.

**Limitación del método:** una muestra dirigida no es estadística. Sirve para evaluar los casos seleccionados, pero no permite proyectar un porcentaje a toda la población.

### 3.3 Procedimiento

1. Obtener el registro (log) de sesiones de descarga del periodo y ordenarlo por número de archivos descargados en 60 minutos.
2. Seleccionar las 10 sesiones de mayor volumen.
3. Para cada sesión, marcar si supera el umbral de 100 archivos.
4. Para las sesiones que superan el umbral, buscar en el SIEM la alerta asociada y calcular el tiempo entre el inicio de la descarga masiva y la alerta.
5. Verificar si la sesión fue bloqueada.
6. **Condición de excepción:** la sesión supera el umbral y (a) no tiene alerta, (b) la alerta llegó después de 15 minutos o (c) la sesión no fue bloqueada.

### 3.4 Evidencia examinada (simulada)

* Extracto del log de sesiones de descarga (CSV ficticio).
* Registros de alertas del SIEM asociados a cada sesión (ficticios).
* Texto de la política simulada PS-CIB-07.

---
## 4. Resultados y hallazgos

### 4.1 Resultados de la prueba (datos ficticios)

| # | Sesión | Cuenta | Fecha | Archivos en 60 min | ¿Supera umbral? | Alerta SIEM | Tiempo a la alerta | ¿Bloqueada? | Resultado |
|---|---|---|---|---:|---|---|---|---|---|
| 1 | S-01 | USR-014 | 8 jul | 412 | Sí | Sí | 6 min | Sí | Cumple |
| 2 | S-02 | USR-203 | 22 jul | 356 | Sí | **No** | — | **No** | **Excepción** |
| 3 | S-03 | USR-087 | 29 jul | 298 | Sí | Sí | 9 min | Sí | Cumple |
| 4 | S-04 | USR-145 | 5 ago | 240 | Sí | Sí | **41 min** | Sí | **Excepción** |
| 5 | S-05 | USR-031 | 14 ago | 187 | Sí | Sí | 4 min | Sí | Cumple |
| 6 | S-06 | USR-260 | 26 ago | 152 | Sí | Sí | 7 min | Sí | Cumple |
| 7 | S-07 | USR-112 | 3 sep | 131 | Sí | Sí | 11 min | Sí | Cumple |
| 8 | S-08 | USR-076 | 12 sep | 96 | No | No | — | No | No aplica |
| 9 | S-09 | USR-190 | 19 sep | 88 | No | No | — | No | No aplica |
| 10 | S-10 | USR-058 | 25 sep | 74 | No | No | — | No | No aplica |

**Lectura de la tabla:**
* 7 de las 10 sesiones superaron el umbral. En 5 de ellas el control operó como exige la política simulada.
* Las 3 sesiones bajo el umbral no generaron alerta, lo cual es correcto según el criterio.
* La tabla **no demuestra** que las descargas de S-02 o S-04 hayan sido maliciosas, ni que el problema exista en toda la población.

### 4.2 Hallazgo H-01: sesión que superó el umbral sin alerta ni bloqueo

| Componente | Contenido |
|---|---|
| **Criterio** | Toda sesión con más de 100 archivos en 60 minutos debe generar alerta en el SIEM en máximo 15 minutos y quedar bloqueada (política simulada PS-CIB-07) |
| **Condición** | La sesión simulada S-02 (cuenta USR-203) descargó 356 archivos en 60 minutos y no registró alerta ni bloqueo |
| **Causa** | Pendiente de confirmar. La prueba no la establece. Habría que revisar, por ejemplo, si la cuenta estaba excluida de la regla de monitoreo o si sus eventos no llegaban al SIEM |
| **Efecto o riesgo** | Una descarga masiva pudo completarse sin que el equipo de seguridad se enterara, que es el mismo tipo de evento del incidente real de julio de 2026 |
| **Recomendación** | Revisar la cobertura de la regla de descargas masivas en el SIEM, incluyendo las cuentas o tipos de cuenta excluidos |

### 4.3 Hallazgo H-02: alerta generada fuera del plazo

| Componente | Contenido |
|---|---|
| **Criterio** | La alerta debe generarse en máximo 15 minutos (política simulada PS-CIB-07) |
| **Condición** | En la sesión simulada S-04 (cuenta USR-145), la alerta se generó 41 minutos después del inicio de la descarga masiva |
| **Causa** | Pendiente de confirmar. La prueba no establece si el retraso viene de la recolección de logs, de la regla de correlación o de la atención de la alerta |
| **Efecto o riesgo** | Durante esos 41 minutos la descarga pudo continuar; el bloqueo tardío reduce la utilidad del control |
| **Recomendación** | Medir los tiempos de cada etapa (recolección, correlación y alerta) para identificar dónde se produce el retraso |


