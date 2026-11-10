# IND-01 — Interfaz UART TTL / RS-485 semidúplex

**3DPS Engineering | Caso de estudio integrado en CTRL-01**  
**Estado:** Tarea 21 aprobada académicamente el 05/11/2026. Diseño revisado con evidencias de KiCad 10. **No fabricado, no ensayado físicamente y no certificado.**

## Necesidad y alcance

Se plantea incorporar comunicación diferencial RS-485 semidúplex al controlador de baja tensión CTRL-01, manteniendo una conexión UART TTL de 3,3 V para diagnóstico. Se documentan selección de interfaz, dirección de transmisión, terminación, rediseño del pinout y verificaciones estáticas. Es un **caso de estudio propio**, no un encargo comercial ejecutado.

## Solución propuesta

- **MCU:** STM32G030K8T6, LQFP32.
- **Transceptor:** TI THVD1410DR, SOIC-8, huella `D0008A_N`.
- **UART:** USART2 TX = PA2 (pin 9, AF1); RX = PA3 (pin 10, AF1).
- **Control de dirección:** RS485_DIR = PA4 (pin 11, GPIO).
- **JP21 y JP22:** selección del camino TTL o RS-485 para TX y RX.
- **JP23 + R22:** terminación de 120 Ω seleccionable; R22 usa `Resistor_SMD:R_1206_3216Metric`, corroborada en el CSV actualizado.
- **R21:** pull-down de control de dirección durante el arranque.
- **R23/R24:** posiciones previstas para polarización, sin montar (DNP) en la variante académica.
- **Bus:** J21 con A, B y GND; puerto TTL local mediante J5.

**Terminación:** en un bus lineal debe colocarse en los dos extremos físicos; la resistencia de este nodo se habilita únicamente cuando corresponda. La polarización externa y el failsafe deben reevaluarse en una instalación real.

## Pinout definitivo de CTRL-01

| Función | Pin MCU | Pin físico | Configuración |
|---|---|---:|---|
| SPI1 MOSI | PB5 | 29 | AF0 |
| SPI1 MISO | PB4 | 28 | AF0 |
| SPI1 SCK | PB3 | 27 | AF0 |
| SPI1 /CS | PA15 | 26 | GPIO (o AF0 según implementación) |
| RELAY_CTRL | PA8 | 18 | GPIO |
| UART TX | PA2 | 9 | USART2 TX, AF1 |
| UART RX | PA3 | 10 | USART2 RX, AF1 |
| RS485_DIR | PA4 | 11 | GPIO |
| MOTOR_PWM | PC6 | 20 | TIM3_CH1, AF1 |
| I²C1 SCL / SDA | PB8 / PB9 | 32 / 1 | AF6 |

## Verificaciones y evidencias

| Comprobación | Evidencia de la T21 |
|---|---|
| Cálculos eléctricos y tiempos | Revisados y aprobados académicamente |
| Esquema y rutas PCB | Capturas de KiCad entregadas |
| Huella U21 | `D0008A_N.kicad_mod` revisada; SOIC-8 de ocho pads y paso 1,27 mm |
| R22 | Captura del símbolo y CSV actualizado con 120 Ω / 1206 |
| ERC | 0 infracciones en captura actualizada |
| DRC | 0 infracciones, 0 elementos sin conectar y 0 errores de paridad, según captura |

Las comprobaciones anteriores están **documentadas a partir de las entregas**. No se atribuye una auditoría automatizada de todos los archivos nativos del proyecto.

## Estado de validación

- **Aprobación académica T21:** completada.
- **Preparación del caso de estudio y documentación:** completada.
- **PCB fabricada y ensamblada:** no.
- **Prueba RS-485 y firmware en hardware:** no acreditada.
- **Medidas eléctricas, EMC, aislamiento y certificaciones:** no realizadas.
- **Disponibilidad como producto industrial o listo para la venta:** no.

En el controlador completo CTRL-01 siguen pendientes comprobaciones ajenas al cierre de T21, entre ellas la selección/huella de C11 (220 µF) y la referencia exacta del fusible F1.

## Capacidades demostradas

Integración de un bus de comunicaciones en un diseño existente, multiplexación y reasignación de pines MCU, configuración de terminación y selección de interfaz, revisión de componentes/huellas y documentación de ERC/DRC.

## Referencias técnicas

- [THVD1410 — Texas Instruments](https://www.ti.com/product/THVD1410)
- [STM32G030K8 — STMicroelectronics](https://www.st.com/resource/en/datasheet/stm32g030k8.pdf)
- [Documentación KiCad 10](https://docs.kicad.org/10.0/)

[Volver a la web 3DPS](https://3dps-engineering.github.io/3DPS/) 

## Continuidad hacia CTRL-01 (09/11/2026)

IND-01 conserva el estado **T21 aprobada académicamente**. El siguiente trabajo del controlador se desarrolla en [CTRL-01 / T22: alimentación y protecciones](../CTRL-01/README.md), **todavía pendiente de aprobación**. La T22 no cambia retrospectivamente las evidencias ni el estado del módulo RS-485.
