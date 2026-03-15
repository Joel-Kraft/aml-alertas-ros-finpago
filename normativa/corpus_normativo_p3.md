# Corpus Normativo — Proyecto 3
## FinPago S.A.S. (PSPCP ficticia) · Sistema de monitoreo AML/KYC

> **Aviso legal:** Este documento forma parte de un portfolio educativo de análisis AML/KYC.
> FinPago S.A.S. es una entidad ficticia creada con fines exclusivamente pedagógicos.
> Todos los casos, clientes, montos y reportes son ficticios. Las normas citadas son reales
> y se referencian con sus URLs oficiales en el Boletín Oficial de la República Argentina.

---

## Índice

1. [Arquitectura normativa del proyecto](#1-arquitectura-normativa-del-proyecto)
2. [Res. UIF N° 200/2024 — Norma base para PSPCP](#2-res-uif-n-2002024--norma-base-para-pspcp)
3. [Res. UIF N° 56/2024 — ROS y definiciones operativas](#3-res-uif-n-562024--ros-y-definiciones-operativas)
4. [Res. UIF N° 207/2025 — RFT y congelamiento](#4-res-uif-n-2072025--rft-y-congelamiento)
5. [Res. UIF N° 3/2026 — RFP y FPADM](#5-res-uif-n-32026--rfp-y-fpadm)
6. [Ley N° 25.246 y modificatorias](#6-ley-n-25246-y-modificatorias)
7. [La distinción que la Res. 56/2024 introduce](#7-la-distinción-que-la-res-562024-introduce)
8. [Cuadro de plazos comparativo](#8-cuadro-de-plazos-comparativo)
9. [Fuentes y URLs de verificación](#9-fuentes-y-urls-de-verificación)

---

## 1. Arquitectura normativa del proyecto

El Proyecto 3 opera bajo un corpus de cuatro normas principales que regulan distintos aspectos
del sistema de prevención de lavado de activos y financiación del terrorismo aplicable a
FinPago S.A.S. en su carácter de Proveedor de Servicios de Pago con Capacidad de Pago (PSPCP).

| Norma | Vigencia | Rol en el proyecto |
|---|---|---|
| Res. UIF N° 200/2024 | Desde 28/06/2024 | Norma base: obliga a FinPago a monitorear transacciones y reportar |
| Res. UIF N° 56/2024 | Desde 26/03/2024 | Define OS/OI, plazos del ROS-LA y estructura del reporte |
| Res. UIF N° 207/2025 | Desde 04/11/2025 | Regula el RFT: plazo, congelamiento inmediato, duración del bloqueo |
| Res. UIF N° 3/2026 | Desde 08/01/2026 | Regula el RFP: cotejo de listas FPADM, plazo y congelamiento |

La norma más reciente del corpus —y la que la mayoría de los candidatos junior desconoce— es
la **Res. UIF N° 207/2025**, vigente desde el 4 de noviembre de 2025. Deroga la Res. 29/2013
y redefine de forma sustancial las obligaciones de reporte y congelamiento para operaciones
de Financiación del Terrorismo.

---

## 2. Res. UIF N° 200/2024 — Norma base para PSPCP

**URL oficial:** https://www.boletinoficial.gob.ar/detalleAviso/primera/308371/20240628

### Qué regula

La Res. UIF N° 200/2024 es la norma de base para los Proveedores de Servicios de Pago con
Capacidad de Pago (PSPCP), categoría en la que se encuadra FinPago S.A.S. como billetera
virtual. Establece los procedimientos mínimos obligatorios de prevención de lavado de activos
y financiación del terrorismo que debe implementar toda entidad de este tipo.

### Obligaciones centrales para el proyecto

**Identificación del cliente:** el sujeto obligado debe identificar y verificar la identidad
de sus clientes en el momento del onboarding, aplicando el esquema de Debida Diligencia (DD)
estándar o Debida Diligencia Reforzada (DDUE) según el perfil de riesgo asignado.

**Perfil transaccional:** cada cliente debe tener un perfil transaccional definido en función
de su actividad declarada, ingresos y comportamiento esperado. Las operaciones que se aparten
de ese perfil activan el sistema de monitoreo.

**Régimen de diferimiento:** los clientes de riesgo bajo ingresan a un período de diferimiento
(hasta 60 días según las condiciones de la norma) durante el cual operan bajo límites reducidos
mientras se completa su calificación formal. El umbral durante el diferimiento es de 15 SMVM.
La superación de ese umbral activa la obligación de completar la calificación con urgencia.

**Monitoreo transaccional:** el sujeto obligado debe implementar un sistema de monitoreo
continuo de las operaciones de sus clientes y generar alertas cuando se detecten comportamientos
inconsistentes con el perfil declarado o con los parámetros del mercado.

**Obligación de reporte:** ante la detección de hechos u operaciones sospechosas, el sujeto
obligado debe reportar a la UIF en los plazos establecidos por la normativa específica
(Res. 56/2024 para ROS-LA; Res. 207/2025 para RFT; Res. 3/2026 para RFP).

---

## 3. Res. UIF N° 56/2024 — ROS y definiciones operativas

**URL oficial:** https://www.boletinoficial.gob.ar/detalleAviso/primera/305169/20240326

### Qué regula

La Res. UIF N° 56/2024 es la norma que define el marco conceptual y operativo del Reporte de
Operación Sospechosa (ROS) para lavado de activos. Introduce dos definiciones que son el eje
conceptual de todo el Proyecto 3: la de **Hecho u Operación Sospechosa** y la de
**Operación Inusual**.

### Definición de Hecho u Operación Sospechosa (HOS)

Aquellas operaciones que, habiéndose analizado, no guardan relación con las actividades lícitas
declaradas por el cliente, o que por su monto, habitualidad u otras características no tienen
una justificación económica o jurídica razonable, o son realizadas sin que medie una actividad
lícita que las justifique.

### Definición de Operación Inusual (OI)

Aquella que se aparta del perfil transaccional del cliente o de los parámetros habituales del
mercado, pero que al ser analizada presenta una explicación razonable y documentada que la
justifica en el marco de la actividad lícita del cliente.

> **Distinción operativa:** la explicación razonable documentada es el único criterio que
> separa una Operación Inusual de un Hecho u Operación Sospechosa. Si existe y es verificable:
> Inusual. Si no existe o no puede verificarse: Sospechosa.

### Plazos del ROS-LA

| Referencia | Plazo | Cómputo |
|---|---|---|
| Plazo estándar | 24 horas | Desde que el sujeto obligado **concluye** que la operación es sospechosa |
| Techo absoluto | 90 días corridos | Desde la **fecha de la operación** observada |

El período de análisis no consume el plazo de 24 horas: el reloj arranca cuando el analista
concluye que hay sospecha. Sin embargo, el techo de 90 días desde la operación es absoluto
e ineludible.

### Estructura del ROS — Las siete preguntas de la guía UIF

La UIF establece que todo ROS debe responder de forma explícita estas siete preguntas:

1. **¿Quién?** — Perfil del cliente: actividad declarada, historial de KYC, nivel de riesgo,
   personas vinculadas.
2. **¿Cuál es la sospecha?** — Descripción del patrón y motivo de sospecha.
3. **¿Qué productos o servicios involucró?** — Productos del sujeto obligado utilizados.
4. **¿Dónde ocurrió?** — Jurisdicción, canal, dispositivos, dirección IP.
5. **¿Cuánto?** — Monto total de las operaciones bajo análisis.
6. **¿Cuáles señales de alerta?** — Referencia al catálogo interno de señales.
7. **¿Cómo se llevó a cabo?** — Mecanismo operativo de la posible maniobra.

Fuente de la guía: https://www.argentina.gob.ar/uif/instructivos/rosrft

### Principio de no alerta

El sujeto obligado no puede informar al cliente que ha sido objeto de un ROS ni que sus
operaciones están siendo investigadas. Este principio es aplicable también durante el análisis
previo al reporte.

---

## 4. Res. UIF N° 207/2025 — RFT y congelamiento

**URL oficial:** https://www.boletinoficial.gob.ar/detalleAviso/primera/333954/20251104

**Vigente desde:** 4 de noviembre de 2025
**Deroga:** Res. UIF N° 29/2013

### Por qué esta norma es un diferenciador

La Res. UIF N° 207/2025 tiene apenas pocos meses de vigencia. La mayoría de los materiales
de estudio disponibles online aún la desconocen o la mencionan superficialmente. Un candidato
que la cita con precisión —y que además explica la diferencia entre el congelamiento por lista
ONU (duración indefinida) y el congelamiento por sospecha de FT (máximo 6 meses prorrogable)—
demuestra un nivel de actualización que supera a la mayor parte de los analistas junior con
experiencia en el mercado.

### Qué regula

La Res. UIF N° 207/2025 redefine drásticamente las obligaciones de los sujetos obligados
frente a operaciones de Financiación del Terrorismo. Ya no alcanza con reportar: en determinadas
circunstancias, el sujeto obligado debe **congelar los activos de forma inmediata** antes de
reportar a la UIF.

### Artículo 1° — Las tres circunstancias que obligan a emitir RFT

El sujeto obligado debe emitir un Reporte de Financiación del Terrorismo cuando:

1. Detecta una operación realizada o tentada que tiene vinculación con personas o entidades
   incluidas en listas de sanciones internacionales relacionadas con terrorismo (OFAC SDGT,
   ONU Res. 1267 y sucesoras, REPET).
2. Recibe una notificación de la UIF sobre una persona o entidad vinculada a actividades
   de FT.
3. Por sus propios medios de análisis, concluye que una operación tiene indicadores de
   financiación del terrorismo, aun sin coincidencia en lista.

### Artículo 2° — Plazo del RFT

**24 horas desde la fecha de la operación realizada o tentada.**

Este plazo es radicalmente distinto al del ROS-LA. No existe tiempo de análisis intermedio:
el reloj corre desde el momento de la operación, no desde la conclusión del análisis.
Esto convierte la detección y el reporte en actos prácticamente simultáneos.

### Artículo 3° — Congelamiento inmediato

Cuando la obligación de reportar surge de una coincidencia en lista (Art. 1°, inciso 1), el
sujeto obligado debe:

1. **Suspender la operación** en curso o bloquear el proceso de onboarding de forma inmediata.
2. **Congelar los activos existentes** del cliente o solicitante en la entidad, sin aviso
   previo al titular.
3. **Reportar a la UIF** dentro de las 24 horas desde la operación.

El orden es ineludible: primero congelar, luego reportar. No es posible reportar sin haber
ejecutado el congelamiento cuando hay coincidencia en lista.

### Duración del congelamiento administrativo

| Circunstancia | Duración del congelamiento |
|---|---|
| Persona o entidad designada en lista internacional (ONU, OFAC) | **Indefinida**, mientras subsista la designación |
| Sospecha de vinculación con FT sin designación previa en lista | **Máximo 6 meses**, prorrogable por única vez |

---

## 5. Res. UIF N° 3/2026 — RFP y FPADM

**URL oficial:** https://www.boletinoficial.gob.ar/detalleAviso/primera/337241/20260108

**Vigente desde:** 8 de enero de 2026

### Qué regula

La Res. UIF N° 3/2026 regula el Reporte de Financiamiento de Proliferación (RFP), que aplica
cuando se detectan operaciones vinculadas a actividades de financiamiento de la proliferación
de armas de destrucción masiva (FPADM: Financiamiento de la Proliferación de Armas de
Destrucción Masiva).

### Plazo del RFP

**24 horas desde la operación realizada o tentada.**

Idéntico al plazo del RFT en su lógica: el reloj corre desde la operación, no desde la
conclusión del análisis.

### Mecanismo de congelamiento FPADM

Análogo al establecido por la Res. 207/2025 para FT: el sujeto obligado debe suspender la
operación y congelar los activos antes de reportar, cuando la obligación de reportar surge
de una coincidencia en las listas de entidades bajo supervisión por proliferación.

### Listas relevantes para el cotejo FPADM

- Listas consolidadas del Consejo de Seguridad de la ONU relacionadas con proliferación
  (Resoluciones específicas sobre Corea del Norte e Irán, entre otras)
- Listas de la OFAC para programas de sanciones por proliferación (NPWMD, DPRK, IRAN)
- Comunicaciones específicas de la UIF sobre entidades bajo supervisión FPADM

---

## 6. Ley N° 25.246 y modificatorias

**Texto vigente (incluye modificaciones Ley N° 27.739):**
https://www.argentina.gob.ar/normativa/nacional/ley-25246-64045

### Artículo 21 — Obligaciones de los sujetos obligados

**Inciso a):** obligación de identificar y conocer al cliente, con los requisitos mínimos
de información que establezca la UIF.

**Inciso b):** obligación de reportar a la UIF, en los términos y plazos establecidos por
la reglamentación, cuando se detecten hechos u operaciones sospechosas de lavado de activos
o financiación del terrorismo. Esta obligación es universal para todos los sujetos obligados
incluidos en el artículo 20 de la ley, con independencia de la norma sectorial aplicable.

> El artículo 21 inciso b) es la norma de jerarquía superior que da fundamento legal a toda
> la obligación de reporte. Las resoluciones de la UIF (56/2024, 207/2025, 3/2026) son la
> reglamentación específica de esa obligación general.

---

## 7. La distinción que la Res. 56/2024 introduce

Esta sección es la más referenciada del repositorio porque explica el cambio conceptual
más relevante del sistema de prevención en los últimos años.

### Antes de la Res. 56/2024

El plazo para reportar una operación sospechosa de lavado de activos era de **15 días corridos**
desde que el sujeto obligado tomaba conocimiento de la operación. La distinción entre
"inusual" y "sospechosa" existía conceptualmente pero no tenía consecuencias operativas
tan precisas.

### Con la Res. 56/2024

El sistema cambia en dos dimensiones simultáneas:

**Primera dimensión — El plazo:**
- ROS-LA: **24 horas** desde la conclusión del análisis (con techo de 90 días desde la operación)
- RFT: **24 horas** desde la operación (sin tiempo de análisis intermedio)
- RFP: **24 horas** desde la operación (sin tiempo de análisis intermedio)

**Segunda dimensión — La distinción conceptual:**
La norma hace operativa la diferencia entre OI y HOS al vincularla con la existencia o
ausencia de explicación razonable documentada. Esto tiene una consecuencia práctica concreta:
el analista no puede clasificar una operación como "inusual" sin documentar explícitamente
cuál es la explicación razonable. La ausencia de documentación equivale, a efectos normativos,
a la ausencia de explicación.

### La Res. 207/2025 agrega una tercera dimensión

Para los casos de FT con coincidencia en lista, la norma introduce la obligación de
congelamiento previo al reporte. Esto significa que el sistema de monitoreo y los
procedimientos internos deben estar diseñados para ejecutar el bloqueo en forma
automática o semi-automática, sin depender de una cadena de aprobaciones que consuma
las pocas horas disponibles antes del vencimiento del plazo.

---

## 8. Cuadro de plazos comparativo

| Tipo de reporte | Sigla | Norma | Evento que activa el plazo | Plazo | Techo absoluto |
|---|---|---|---|---|---|
| Reporte de Operación Sospechosa de LA | ROS-LA | Res. 56/2024 | Conclusión del análisis (el SO determina que hay sospecha) | 24 horas | 90 días corridos desde la operación |
| Reporte de Financiación del Terrorismo | RFT | Res. 207/2025 | Fecha de la operación realizada **o tentada** | 24 horas | No puede exceder las 24 horas |
| Reporte de Financiamiento de Proliferación | RFP | Res. 3/2026 | Fecha de la operación realizada **o tentada** | 24 horas | No puede exceder las 24 horas |

> **Diferencia operativa crítica:** para el ROS-LA, el analista tiene tiempo de analizar
> antes de que el reloj del plazo comience a correr. Para RFT y RFP, el reloj corre desde
> el momento de la operación, lo que exige detección y reporte prácticamente simultáneos.

---

## 9. Fuentes y URLs de verificación

Todas las normas citadas en este repositorio son de acceso público. A continuación se listan
las fuentes utilizadas para la verificación del corpus normativo.

| Norma | URL Boletín Oficial | Fuente adicional |
|---|---|---|
| Res. UIF N° 200/2024 | https://www.boletinoficial.gob.ar/detalleAviso/primera/308371/20240628 | — |
| Res. UIF N° 56/2024 | https://www.boletinoficial.gob.ar/detalleAviso/primera/305169/20240326 | https://www.argentina.gob.ar/uif |
| Res. UIF N° 207/2025 | https://www.boletinoficial.gob.ar/detalleAviso/primera/333954/20251104 | — |
| Res. UIF N° 3/2026 | https://www.boletinoficial.gob.ar/detalleAviso/primera/337241/20260108 | — |
| Ley N° 25.246 (mod. 27.739) | https://www.argentina.gob.ar/normativa/nacional/ley-25246-64045 | — |
| Guía UIF — Cómo completar un ROS | https://www.argentina.gob.ar/uif/instructivos/rosrft | Documento oficial UIF |

---

*FinPago S.A.S. es una entidad ficticia creada con fines educativos.*
*Normativa: Res. UIF N° 200/2024 · 56/2024 · 207/2025 · 3/2026 · Ley N° 25.246 (mod. 27.739)*
*Portfolio AML/KYC  — Joel Kraft — https://www.linkedin.com/in/kraft-joel-analytics/*