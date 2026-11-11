# T22 — Corriente en régimen y coordinación de F1

**CTRL-01 / 3DPS Engineering**  
**Referencia de trabajo:** 9 de noviembre de 2026 (T22 abierta).  
**Revisión documental añadida:** 11 de noviembre de 2026.

> **Importante:** aquí se reúnen las cifras que constan en el informe académico de T19, en el formulario de T22 y en el CSV actualizado que se utilizó en T21. No se ha localizado una entrega de resultados de T22 que permita atribuir al lunes 9 una medición ni un cálculo adicional definitivo. La T22 **no está aprobada**.

## 1. Qué entendemos por corriente «en régimen»

La **corriente en régimen permanente** es la corriente que el sistema demanda cuando sus cargas han alcanzado un estado de funcionamiento estabilizado bajo una condición especificada (por ejemplo, MCU activa, motor a un determinado PWM y relé en un estado conocido). **No debe confundirse** con:

- **Pico de arranque:** al conectar la fuente o al arrancar motor/condensadores; depende de su dinámica y puede durar muy poco.
- **Máximo normal de diseño:** combinación de cargas prevista sin fallo, que puede ser mayor que la corriente nominal típica.
- **Corriente de bloqueo o defecto:** motor bloqueado o cortocircuito; requiere un análisis separado y **no se ha medido**.
- **Límite de fuente de 2 A:** máximo que la alimentación declara limitar, no una corriente que necesariamente consuma CTRL-01.

Los siguientes números son **hipótesis del informe T19 aprobado académicamente** y todavía necesitan comprobarse con cargas definidas y, en su caso, prototipo:

| Magnitud | Valor | Procedencia / carácter |
| --- | ---: | --- |
| Corriente nominal de entrada de diseño | **0,45 A** | T19, cálculo C1; hipótesis |
| Corriente máxima de diseño | **0,95 A** | T19, cálculo C2; hipótesis, **no corriente de bloqueo medida** |
| Tensión nominal de entrada | **12 V CC** | Condición del ejercicio |
| Límite declarado de la fuente | **2,00 A** | Hipótesis del proyecto, no ensayo |
| Temperatura de referencia de la fuente / entorno | **20–30 °C** | Condición declarada en T19 |

Por tanto, en T22 **C1 continúa pendiente de actualizar** con una suma por ramas: entrada 12 V, motor, bobina del relé, regulador 3,3 V y cualquier otra carga realmente conectada. No basta con copiar 0,45 A sin justificar estados, eficiencia, márgenes o simultaneidad.

## 2. Referencias de F1 que aparecen en la documentación

**Hay una discrepancia que no debe ocultarse:**

| Referencia identificada | `Ihold` nominal | `Itrip` nominal | Fuente |
| --- | ---: | ---: | --- |
| **Littelfuse 2016L150DR** | **1,50 A** | **3,00 A** | Informe aprobado T19 y hoja de datos Littelfuse |
| **Littelfuse 2016L050MR** | **0,55 A** | **1,10 A** | Nombre de la huella F1 en el CSV de T21; hoja de datos Littelfuse |

En el **último CSV exportado** la fila es `F1, Fuse, FUSER_2016L050MR:FUSER_2016L050MR`. Esto identifica el nombre de huella del proyecto, **pero no confirma por sí solo el MPN definitivo de compra** ni el comportamiento del montaje. La referencia del símbolo es genérica (`Fuse`), así que se exige decidir el componente exacto y alinear esquema, huella y BOM.

Referencia del fabricante: [Littelfuse, familia 2016L — hoja de datos](https://www.littelfuse.com/assetdocs/resettable-ptcs-2016l-datasheet?assetguid=0a3f187e-62df-469f-85be-57fe3e3b4668).

## 3. Comparación con las corrientes de diseño

Los cocientes siguientes son **comparaciones estáticas con Ihold nominal**, no predicciones del tiempo de disparo:

| Situación | Corriente | % de Ihold 2016L050MR (0,55 A) | % de Ihold 2016L150DR (1,50 A) |
| --- | ---: | ---: | ---: |
| Régimen nominal hipotético | 0,45 A | 81,82 % | 30,00 % |
| Máximo de diseño hipotético | 0,95 A | **172,73 %** | 63,33 % |
| Límite de fuente declarado | 2,00 A | 363,64 % | 133,33 % |

**Interpretación:**

- **2016L050MR:** a 0,45 A queda un margen nominal de **0,10 A** frente a Ihold (sin desclasificación por temperatura). La hipótesis de 0,95 A **supera** Ihold; podría causar calentamiento o disparos intempestivos según temperatura, duración y curva, aunque 0,95 A siga por debajo del Itrip nominal de 1,10 A. No se puede afirmar un disparo seguro a esa corriente.
- **2016L150DR:** 0,95 A es inferior a Ihold nominal. Sin embargo, **2,00 A está por debajo de Itrip = 3,00 A**, así que un suministro limitado a 2 A **no garantiza el disparo** del PTC. La fuente sería el elemento principal de limitación de cortocircuito según las hipótesis de T19.
- **Ambos:** un PPTC no equivale a un fusible convencional de apertura permanente. Necesita analizar curva tiempo-corriente, temperatura ambiente, tensión y corriente máximas, energía disponible, cableado y fallo de TVS.

**No seleccionar F1 solo con esta tabla:** se necesita confirmar la corriente real en régimen, el perfil transitorio, el estado del motor, la resistencia térmica y el entorno.

## 4. Cálculos relacionados previstos en el formulario T22

Estos valores son **autocontroles del formulario**, no una entrega de respuestas del alumno ni medidas de laboratorio:

| Cálculo | Hipótesis | Resultado de referencia |
| --- | --- | ---: |
| C2 — caída de entrada | 1,50 A × 0,12 Ω | **0,18 V** |
| C3 — pérdida en el camino resistivo | (1,50 A)² × 0,12 Ω | **0,27 W** |
| C4 — energía ideal C11 | ½ × 220 µF × (12 V)² | **15,84 mJ** |
| C5 — sostén ideal | 220 µF × (12−10 V)/0,20 A | **2,20 ms** |
| C6 — reactancia ideal | 220 µF a 100 kHz | **≈7,23 mΩ** (sin ESR/ESL) |
| C7 — rizado ESR aproximado | 0,40 A × 0,15 Ω | **60,00 mV** |

C8 (presupuesto de corriente a 3,3 V), C9 (pérdidas del regulador), C10 (selección real C11), C11 (especificación F1) y C12 (pistas/vías) **no tienen respuesta final verificada**.

## 5. Qué queda por hacer en KiCad 10

1. Abrir la última versión del proyecto CTRL-01, identificar en esquema si **F1** corresponde a un PPTC u otro componente y comprobar MPN, huella y BOM. La diferencia entre `2016L050MR` y `2016L150DR` no se resuelve por el nombre de la huella.
2. Desglosar el **consumo en régimen** por cargas y escenarios (MCU/3,3 V, relé energizado, motor a PWM definido); contemplar simultaneidad y rendimiento del regulador.
3. Estimar picos de conexión, arranque y posible corriente de bloqueo del motor **por separado**, sin confundirlos con los valores de 0,45/0,95 A.
4. Revisar C11 de 220 µF en 0805 (tecnología, tensión, capacidad efectiva, ripple/ESR y MPN).
5. Confirmar la curva tiempo-corriente y la desclasificación térmica de F1. Analizar la coordinación con fuente 12 V limitada a 2 A, protección TVS SMBJ15A y Schottky SS34, incluyendo caminos de fallo.
6. Actualizar esquemático, PCB, reglas de potencia y BOM; ejecutar ERC/DRC **después** de aplicar los cambios. Entregar resultados y justificaciones antes de aprobar T22.

## Estado de evidencias

- **T19:** informe académico aprobado, hipótesis y cálculos documentados.
- **T21:** aprobación académica y CSV posterior donde se identifica la huella `2016L050MR`.
- **T22:** formulario de ejercicio disponible; **sin entrega final corregida o aprobada**, sin ERC/DRC nuevos acreditados, sin corriente de régimen medida.
- **CTRL-01:** no existe evidencia de PCB fabricada, prototipo validado o certificación.

[Volver al README CTRL-01](README.md) · [Registro del 9/11](AVANCES_2026-11-09.md)
