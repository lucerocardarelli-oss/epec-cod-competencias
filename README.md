# Matriz de Competencias — CCOD (EPEC S.A.U.)

**Qué hace:** evaluación técnica (planillas por puesto + procesos compartidos) y de liderazgo, autoevaluación, evaluación de equipo, feedback, plan de acción (con sugerencias), historial, radar, tendencia, Nine Box, ficha por persona, guía de puestos, informe ejecutivo y respaldo de datos. Tema claro/oscuro (sol/luna).

## Procesos según el Manual de Procesos CCOD v1.2 (13/10/2026)
- Catálogo con los nombres, finalidad y salida clave del manual: P-JCOD-01..05, P-SCOD-01..03, P-JTMT-01..03 y P-OMT-01..03 (**Operador MT es ahora un puesto evaluable**), más los 2 procesos complementarios del Subjefe (sin código institucional; el id P-SCOD-04/05 es solo interno).
- **P-DUP-01..15 y P-TEC-01 no figuran en el manual**: se conservan marcados como "fuera del manual".
- **SHyMA / Expertiz**: en el manual SHyMA es un área a la que se consulta, no un proceso. La evaluación transversal pasa a **Seguridad operacional (control operacional y SG-P200)**. Los procesos de seguridad son P-JTMT-02, P-OMT-03 y P-TEC-02: una calificación 1 genera una **alerta de seguridad operacional** (se revisa con el tutor y se registra una acción); **ya no bloquea ni marca "no habilitado"**. Los datos viejos conservan el campo interno `shyBad`.

## Estructura de pestañas (v. 29/10/2026)
- **Dashboard** · **Evaluar persona** (Resumen y evolución / Técnica / Liderazgo y autoevaluación, un solo guardado) · **Evaluación de Equipo** · **Feedback y Plan** (un solo selector de persona) · **Análisis** (Radar / Tendencia / Historial) · **Nine Box** · **Guía de puestos** · **Reportes PDF**.
- **Un solo registro por persona + puesto + instancia**: la técnica, el liderazgo, la autoevaluación y las evidencias se guardan juntos. Si una persona tenía datos repartidos en varios registros de la misma instancia, se muestran unidos y se ofrece el botón **Unificar en un solo registro** (pide confirmación antes de eliminar los duplicados).
- **Limpiar** en cada pestaña con datos o filtros: deja la pantalla lista para una nueva evaluación.
- Instancias: Diagnóstico, Seguimiento, Certificación.

## Guardar la pantalla en la computadora
Botón **Guardar pantalla** (encabezado, junto al sol/luna): guarda lo que se ve en la pantalla actual como **PDF** (A4, con cortes de página que no parten tarjetas ni filas), **imagen PNG** o **página HTML**. Siempre en tema claro, aunque se esté usando el oscuro. En Reportes y en el reporte de Plan de Acción guarda la vista previa generada. En celular guarda con el diseño de computadora. Requiere internet (usa las librerías html2canvas y jsPDF).

## Funciones principales
- **Puestos y procesos:** según *Descripción de Puestos CCOD v1.1* y *Procesos de Trabajo Roles*. Códigos internos JCOD/SCOD/JTMT (Coordinador de Turno MT = antes Jefe de Turno). P-SCOD-04/05 son códigos provisorios.
- **Nivel esperado** por puesto e instancia (`ESPERADO` en `index.html`): valores de referencia a validar. Se usan en fichas, alertas, plan de acción e informe.
- **Evidencia** por proceso/competencia, **autoevaluación** de liderazgo y **autoría** (quién cargó/modificó, con la cuenta de ingreso).
- **Pendientes de seguimiento** en el Dashboard: SHyMA, acciones vencidas, bajo lo esperado, reevaluación (`REEVAL_DIAS` = 21), mediciones incompletas.
- **Plan de acción**: botón "Sugerir acciones" (borrador editable; no pisa lo escrito).
- **Reportes**: informe ejecutivo (resumen para Gerencia) y respaldo CSV/JSON.

## Parámetros editables (al inicio del script, sección "PARÁMETROS EDITABLES")
`ESPERADO`, `REEVAL_DIAS`, `ENABLE_MS_LOGIN`, `MS_TENANT`.

## Login con cuenta EPEC (Microsoft Entra ID)
Está **apagado** (`ENABLE_MS_LOGIN = false`). Para activarlo: (1) EPEC registra una aplicación en Entra ID con la URI de redirección que muestra Firebase; (2) Firebase Console → Authentication → Sign-in method → Microsoft: cargar Application (client) ID y secreto; (3) poner `ENABLE_MS_LOGIN = true` (y `MS_TENANT` con el ID de directorio de EPEC) y subir el archivo. El email/contraseña sigue disponible para personas externas.

## Reglas de seguridad de Firebase
`reglas-firebase-cod.json` contiene las reglas de los nodos `cod_*` (solo usuarios con sesión no anónima; valida puesto —incluido OMT— y promedios 0–4). **No reemplazar las reglas completas**: el proyecto lo comparten otras apps. Copiar solo esos nodos dentro de `rules` en Firebase Console → Realtime Database → Reglas. Probarlas antes con el simulador.

## Despliegue
GitHub → repo `epec-cod-competencias` → Add file → Upload files → `index.html` (nombre exacto) → Commit. GitHub Pages publica en 1–2 minutos.

## Cuentas asociadas
Firebase `epec---capacitaciones` (Auth + Realtime Database) y GitHub Pages `lucerocardarelli-oss`. Sin agente de IA ni API de Anthropic.

## Límites
Pensada para un equipo chico (decenas de usuarios simultáneos). El plan gratuito de Firebase limita conexiones simultáneas y descarga de datos; si crece el uso conviene plan Blaze o migrar a una base con control de acceso por grupo.
