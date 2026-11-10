# CTRL-01 — Controlador electrónico modular de baja tensión

**3DPS Engineering · Caso de estudio propio, integración progresiva en KiCad 10**

> **Estado al 9 de noviembre de 2026:** módulos de ejercicios hasta T21 aprobados académicamente; **T22 en curso y pendiente de entrega/corrección**. No consta placa fabricada, prototipo probado físicamente ni certificación. Este repositorio documenta competencias de diseño, no un producto disponible para venta.

[Ver página del proyecto](https://3dps-engineering.github.io/3DPS/proyectos/CTRL-01/) · [Subsistema IND-01 / RS-485](../IND-01/README.md) · [Web 3DPS](https://3dps-engineering.github.io/3DPS/)

## Necesidad técnica

Desarrollar por etapas el esquema y el layout de un controlador de **baja tensión**, documentando decisiones reutilizables y verificando cada bloque antes de integrar funcionalidades adicionales. El trabajo funciona como caso de estudio de ingeniería para posibles encargos de esquemáticos, PCB y prototipado; **no representa un pedido ejecutado para un cliente externo**.

## Arquitectura y subsistemas trabajados

| Bloque | Alcance formativo documentado | Estado |
| --- | --- | --- |
| MCU | STM32G030K8T6 (LQFP32), redistribución de pines y buses | Revisión académica hasta T21 |
| I²C | Sensor TMP102, resistencias pull-up, cálculos de tiempo de subida | T15 aprobada |
| SPI | Memoria W25Q32 de 32 Mbit, señales de selección y temporización | T16 aprobada |
| Actuadores | Control de relé de 12 V y PWM de motor | T17–T18 aprobadas |
| Protección de alimentación | TVS, PTC/fusible y límites eléctricos | T19 aprobada; auditoría global pendiente |
| UART / ESD | Conector UART 3,3 V y protección ESD | T20 aprobada |
| RS-485 | THVD1410DR, jumpers TTL/RS-485 y terminación | T21 aprobada como [IND-01](../IND-01/README.md) |
| Alimentación y protecciones | Condensador C11, fusible F1, pistas de potencia y retorno | **T22 abierta, no aprobada** |

La aprobación de un bloque implica **evaluación académica de los cálculos y evidencias aportadas**, no que el controlador integrado haya sido verificado en laboratorio.

## Hito del 9 de noviembre de 2026 — T22

### Objetivo y alcance

Se mantuvo abierta la tarea **T22: auditoría de alimentación de 12 V y 3,3 V y protecciones de CTRL-01**. El material de trabajo plantea:

1. **C11:** confirmar valor nominal de 220 µF, tecnología, tensión, ESR, corriente de rizado y dimensiones físicas. La asociación de 220 µF con una huella 0805 requiere justificar un componente concreto; no se considera resuelta por defecto.
2. **F1:** identificar referencia comercial real, curva tiempo-corriente, corriente de mantenimiento/disparo o calibre nominal según tipo y coordinación con alimentación, pistas y protección.
3. **Presupuesto de corriente y potencia:** justificar consumo de cargas a 12 V y a 3,3 V, pérdidas, caídas de tensión, rizado y márgenes, usando hipótesis explícitas.
4. **PCB:** revisar anchuras de rutas de alimentación, retornos de corriente, desacoplos y zonas GND; diferenciar diseño de potencia de señales de control.
5. **Verificación:** actualizar esquema y BOM; ejecutar ERC/DRC **después** de cualquier cambio y aportar evidencias.

### Actividad realmente documentada el 09/11

- Continuidad de la T22 sin pasar a T23.
- Material del ejercicio preparado con **12 cálculos, 6 preguntas técnicas y revisión de PCB**.
- Incidencia informada por el usuario: el enlace de descarga del ZIP T22 no respondía; se inició la revisión de esa entrega. **No debe confundirse con una corrección de la PCB o una aprobación técnica.**
- **No consta** entrega de resultados T22 ni nueva evidencia ERC/DRC que permita aprobar esta auditoría.

Se conserva el registro cronológico: [Avances del 9 de noviembre](AVANCES_2026-11-09.md).

## Criterios para aprobar la T22

- [ ] Identificación de C11 por referencia de fabricante y huella compatible, con cálculos eléctricos documentados.
- [ ] Selección justificada de F1 y sus límites de protección.
- [ ] Cálculos completos de corriente, potencia, rizado y caídas de tensión, con unidades.
- [ ] Revisión del esquema y actualización del PCB en KiCad 10, cuando proceda.
- [ ] BOM coherente con los componentes revisados.
- [ ] ERC y DRC finales sin infracciones relevantes, con evidencias fechadas.
- [ ] Informe de diagnóstico y ZIP de entrega revisado.

Solo después de la aprobación se incorporarán al portfolio conclusiones de diseño verificadas y el informe PDF final de esa tarea.

## Alcance comercial y nivel de evidencia

| Nivel | Situación del caso |
| --- | --- |
| Curso y ejercicios aprobados | Hasta T21 |
| T22 — alimentación y protecciones | **En curso** |
| Verificación global de CTRL-01 | No acreditada |
| Fabricación de PCB | No acreditada |
| Ensayos físicos / firmware validado | No acreditados |
| EMC, seguridad, normativa y certificación | No acreditadas |

**No se publican Gerbers, instrucciones de fabricación ni listas de montaje definitivas** como si fueran aptas para producción. Los trabajos de cliente requerirían requisitos, revisión específica y aceptación contractual propios.

## Evidencias de 3DPS

Las pruebas académicas del subsistema de comunicaciones se describen en [IND-01](../IND-01/README.md). Para la T22 aún están **pendientes** los resultados y capturas verificadas de esquema, PCB, BOM y ERC/DRC, junto con el informe de cierre. No se inventan medidas ni simulaciones.

## Referencias principales

- [STM32G030K8 — STMicroelectronics](https://www.st.com/resource/en/datasheet/stm32g030k8.pdf)
- [Documentación KiCad 10](https://docs.kicad.org/10.0/)
- [THVD1410 — Texas Instruments](https://www.ti.com/product/THVD1410)
