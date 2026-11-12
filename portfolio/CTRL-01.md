# CTRL-01 | Estudio de protección y alimentación de una placa de control

**3DPS Engineering · Caso de entrenamiento técnico · 12/11/2026**

## Objetivo
Evaluar, en un ejercicio académico, el comportamiento de la alimentación de una placa de control de 12 V: consumo estacionario, arranque, protección rearmable frente a sobrecorriente, supresión de transitorios y caída resistiva en la alimentación.

## Alcance y decisiones
- Alimentación de laboratorio regulada a 12 V; límite de corriente de 5 A adoptado como hipótesis del estudio.
- Protección de sobrecorriente: PPTC Littelfuse **2016L150DR (F1)**.
- Protección de sobretensiones transitorias: TVS **SMBJ15A (D19)**, situado aguas abajo de F1.
- Desacoplo y reserva local: **C11, 220 µF / 50 V**.
- Se conservaron sin cambios el esquemático, la PCB y las clases de red del ejercicio anterior.
- Los cálculos académicos se revisaron y la tarea se cerró bajo sus hipótesis. Esto **no constituye certificación para fabricación ni ensayo de seguridad**.

## Trabajo realizado
Análisis de régimen permanente, arranque, limitación de corriente, respuesta térmica conceptual de un PPTC, efecto de la ESR y comprobación teórica de pérdidas en la alimentación. Se documentaron por separado los valores supuestos y los datos de catálogo.

## Entregables y confidencialidad
Esta ficha resume el alcance y las decisiones del caso sin publicar archivos fuente de KiCad, topología completa, distribución de componentes, respuestas detalladas ni documentación que permita reproducir directamente el diseño.

**Estado:** ejercicio académico completado; sin cambios de PCB respecto al ejercicio anterior.
