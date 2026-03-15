# Análisis de Alertas y Reportes de Operaciones Sospechosas
**Portfolio AML/KYC · Ejercicio con datos simulados**

## Descripción

Este proyecto construye un sistema completo de monitoreo transaccional y análisis de señales
de alerta para FinPago S.A.S., una billetera virtual ficticia encuadrada como Proveedor de
Servicios de Pago con Capacidad de Pago (PSPCP) bajo la Res. UIF N° 200/2024. El ejercicio
cubre el proceso de punta a punta: desde la detección de un comportamiento que activa una
señal del catálogo hasta la decisión de clasificar la operación como Inusual o Sospechosa,
y la emisión del reporte correspondiente (ROS-LA, RFT o RFP) dentro de los plazos normativos
vigentes. El objetivo es demostrar la capacidad de traducir el marco regulatorio en
herramientas operacionales reproducibles: un catálogo de señales con respaldo normativo,
informes de análisis estructurados según el formato oficial de la UIF, un log de casos con
fórmulas de control de plazo, y un dashboard de monitoreo de cola de alertas en Power BI.

---

## Marco normativo aplicado

| Norma | Disposiciones clave | Enlace |
|---|---|---|
| Res. UIF N° 200/2024 | Norma base para PSPCP: monitoreo transaccional, perfil de riesgo, régimen de diferimiento (umbral 15 SMVM), obligación de reporte | [Ver en BO](https://www.boletinoficial.gob.ar/detalleAviso/primera/308371/20240628) |
| Res. UIF N° 56/2024 | Definición de Hecho u Operación Sospechosa y Operación Inusual; plazo ROS-LA: 24 hs desde la conclusión / máx. 90 días desde la operación; estructura del ROS (7 preguntas) | [Ver en BO](https://www.boletinoficial.gob.ar/detalleAviso/primera/305169/20240326) |
| Res. UIF N° 207/2025 | Deroga Res. 29/2013. Regula el RFT: plazo 24 hs desde la operación realizada o tentada; congelamiento inmediato obligatorio antes del reporte cuando hay coincidencia en lista; duración del congelamiento: indefinida (designados ONU/OFAC) o máx. 6 meses prorrogable (sospecha de FT). Vigente desde 04/11/2025 | [Ver en BO](https://www.boletinoficial.gob.ar/detalleAviso/primera/333954/20251104) |
| Res. UIF N° 3/2026 | Regula el RFP: plazo 24 hs desde la operación; mecanismo de congelamiento FPADM; cotejo de listas internacionales de proliferación. Vigente desde 08/01/2026 | [Ver en BO](https://www.boletinoficial.gob.ar/detalleAviso/primera/337241/20260108) |
| Ley N° 25.246 (mod. 27.739) | Art. 21 inc. b): obligación universal de reporte sin demora para todos los sujetos obligados | [Ver texto](https://www.argentina.gob.ar/normativa/nacional/ley-25246-64045) |

---

## Contenido del repositorio

| Archivo | Descripción | Formato |
|---|---|---|
| `normativa/corpus_normativo_p3.md` | Compendio de normas citadas con artículos, plazos y URLs de verificación | Markdown |
| `catalogo/catalogo_25_senales_alerta.xlsx` | 25 señales clasificadas en 5 categorías con tipo de reporte, nivel de urgencia y fuente normativa | Excel |
| `casos/CASO_01_Fraccionamiento_ROS_LA.pdf` | Fraccionamiento hacia múltiples beneficiarios → ROS-LA | PDF |
| `casos/CASO_02_PEP_Inusual.pdf` | PEP activo, transferencia de organismo público → Operación Inusual (sin ROS) | PDF |
| `casos/CASO_03_Criptoactivos_ROS_LA.pdf` | Conversiones fiat→cripto inconsistentes con perfil bajo → ROS-LA | PDF |
| `casos/CASO_04_Lista_OFAC_RFT.pdf` | Coincidencia 87% en lista OFAC durante onboarding → congelamiento + RFT (Res. 207/2025) | PDF |
| `casos/CASO_05_Transferencias_Internacionales_ROS_LA.pdf` | Transferencias a jurisdicción GAFI sin justificación comercial → ROS-LA | PDF |
| `log/LOG_CASOS_FINPAGO.xlsx` | Log de 20 casos (Sep 2025 – Feb 2026) con fórmulas de días de análisis y control de plazo normativo | Excel |
| `arbol_decision/arbol_decision_ros.pdf` | Lógica de clasificación: dos niveles de decisión, cuatro salidas posibles, con base normativa por rama | PDF |
| `arbol_decision/arbol_decision_ros.png` | Versión visual del árbol (Canva, 1920×1080 px) | PNG |
| `dashboard/pagina1_cola_operacional.png` | Vista operacional: tarjetas de indicadores, tabla de casos abiertos, gráfico de decisiones | PNG |
| `dashboard/pagina2_gerencial.png` | Vista gerencial: cumplimiento de plazos, distribución por tipo de reporte, tendencia mensual 6 meses | PNG |
| `dashboard/dashboard_alertas.pbix` | Archivo fuente Power BI (2 páginas, 7 medidas DAX) | PBIX |
| `infografia/distincion_inusual_sospechosa.png` | Comparativo visual Operación Inusual vs. Hecho u Operación Sospechosa (Canva, 1080×1350 px) | PNG |

---

## Cómo navegar el proyecto

1. **Empezá por el corpus normativo** (`normativa/`) — explica los plazos diferenciados por tipo de reporte y la distinción conceptual que la Res. 56/2024 introduce entre Operación Inusual y Hecho u Operación Sospechosa
2. **Revisá el catálogo de señales** (`catalogo/`) — 25 señales con su tipo de reporte asociado; las SAL-018 y SAL-019 activan el protocolo de congelamiento inmediato de la Res. 207/2025 y la Res. 3/2026
3. **Leé el Caso 04** (`casos/`) — el de mayor complejidad técnica: coincidencia en lista OFAC durante onboarding → suspensión automática → congelamiento inmediato → RFT en 24 hs desde la operación tentada
4. **Abrí el log** (`log/`) — 20 casos del período con la columna `PLAZO_CUMPLIDO` calculada automáticamente según el tipo de reporte
5. **Explorá el dashboard** (`dashboard/`) — las capturas muestran ambas páginas; el `.pbix` permite interactividad completa en Power BI Desktop

---

## Limitaciones

Todos los clientes, montos, fechas, números de reporte y resultados de cotejo en listas
utilizados en este proyecto son ficticios y fueron generados exclusivamente con fines
educativos. FinPago S.A.S. no existe y no tiene ningún vínculo con ninguna entidad financiera
real. Las normas citadas son reales y verificables en las URLs indicadas; su interpretación
en este ejercicio es propia y no ha sido validada por ninguna autoridad regulatoria.
Ver [DISCLAIMER.md](DISCLAIMER.md).

---

## Autor

**Joel Kraft** · https://www.linkedin.com/in/kraft-joel-analytics/