# LABORATORIO 2: Estimación del nivel de estrés basaada en la respuesta galvánica cutánea GSR
# INTRODUCCIÓN
El estrés es una respuesta fisiológica del organismo ante estímulos que requieren atención, esfuerzo mental o adaptación. Durante estos procesos se activa el sistema nervioso autónomo, especialmente el sistema nervioso simpático, lo que genera diferentes cambios fisiológicos en el cuerpo humano. Uno de estos cambios es la variación en la actividad de las glándulas sudoríparas, la cual puede medirse a través de la conductancia eléctrica de la piel.

La respuesta galvánica cutánea (GSR) es una técnica utilizada para registrar estas variaciones en la conductancia de la piel, permitiendo observar cambios asociados a estímulos emocionales, cognitivos o fisiológicos. Debido a su sensibilidad frente a la activación autonómica, la GSR se ha convertido en una herramienta ampliamente utilizada en estudios de psicofisiología y en el desarrollo de dispositivos biomédicos para el monitoreo del estrés. 

En esta práctica se propone diseñar e implementar un dispositivo vestible capaz de medir la respuesta galvánica cutánea y visualizar la señal en tiempo real. A través de este sistema se busca analizar cómo varía la conductancia de la piel cuando una persona realiza diferentes actividades o experimenta cambios en su estado fisiológico.
# FUNDAMENTOS TEÓRICOS
La actividad electrodérmica (EDA) se refiere a los cambios en las propiedades eléctricas de la piel que ocurren como consecuencia de la actividad del sistema nervioso autónomo. Uno de los fenómenos más estudiados dentro de esta actividad es la respuesta galvánica cutánea (GSR), la cual corresponde a variaciones en la conductancia eléctrica de la piel asociadas principalmente a la activación del sistema nervioso simpático. Este sistema regula funciones involuntarias del organismo, incluyendo la actividad de las glándulas sudoríparas, cuya secreción influye directamente en la conductividad eléctrica de la piel. 

Cuando una persona experimenta estímulos emocionales, cognitivos o fisiológicos (estrés, dolor o una respiración profunda) se produce una activación del sistema nervioso simpático que incrementa la actividad de las glándulas sudoríparas ecrinas. Este aumento de sudoración modifica la resistencia eléctrica de la piel y genera un incremento en su conductancia. Debido a esta relación fisiológica, la GSR se utiliza ampliamente como un indicador indirecto del nivel de activación emocional o cognitiva de una persona.

La señal de conductancia cutánea suele analizarse a partir de dos componentes principales. El nivel de conductancia cutánea (Skin Conductance Level, SCL) representa el nivel basal de conductancia de la piel, el cual varía lentamente en el tiempo y refleja el estado general de activación fisiológica del individuo. Por otro lado, la respuesta de conductancia cutánea (Skin Conductance Response, SCR) corresponde a cambios rápidos y transitorios que se producen frente a estímulos específicos. Estas respuestas se caracterizan por un aumento rápido en la conductancia seguido de una recuperación más lenta hacia el nivel basal, comportamiento que ha sido ampliamente reportado en estudios de psicofisiología. 

Debido a su sensibilidad frente a cambios en la actividad autonómica, la GSR se ha utilizado en múltiples aplicaciones dentro de la ingeniería biomédica y la psicofisiología, incluyendo el estudio del estrés, la evaluación de respuestas emocionales, la investigación en toma de decisiones y el desarrollo de dispositivos portátiles de monitoreo fisiológico. Sin embargo, aunque la GSR es un indicador útil de activación simpática, su interpretación debe considerar factores externos como la temperatura, la humedad o el movimiento del sujeto, los cuales también pueden afectar las mediciones.

## Efectos de la corriente en el cuerpo humano
El paso de corriente eléctrica por el cuerpo humano, en ocasiones suele producir diferentes efectos fisiológicos dependiendo de la intensidad de la corriente, el tiempo de exposición, si la corriente es directa o alterna y el trayecto que va a seguir en el cuerpo humano.

Para corrientes pequeñas, menores a 1 mA, generalmente no se presentan efectos fisiológicos perceptibles. Sin embargo, al aumentar la corriente pueden aparecer sensaciones de hormigueo, contracciones musculares e incluso riesgo de fibrilación ventricular en corrientes elevadas.

En aplicaciones biomédicas que implican contacto eléctrico con el cuerpo humano, es fundamental garantizar que la corriente que atraviesa el organismo sea extremadamente baja. Por esta razón, en sistemas de medición fisiológica como el utilizado en esta práctica, se limita la corriente a valores inferiores a 1 mA, garantizando condiciones seguras para el sujeto.
## Cálculos de seguridad del circuito
El sistema propuesto para la medición de la respuesta galvánica cutánea se alimenta con una fuente de voltaje baja, entre 3.3 V y 5 V. Debido a que el dispositivo entra en contacto directo con el cuerpo humano, es de vital importancia garantizar que la corriente que circula a través de la piel del usuario se mantenga dentro de límites seguros.

En el circuito, la corriente queda limitada por la resistencia **R1 = 68 kΩ** y por la resistencia de la piel $R_{\text{piel}}$.

La ecuación general que describe la corriente es:

$$
I=\frac{V_{CC}-V_{EE}}{68\k\Omega + R_{\text{piel}}}
$$

Para verificar la seguridad del circuito se analiza el caso extremo:

$$
R_{\text{piel}} = 0
$$

Sustituyendo en la ecuación:

$$
I=\frac{V_{CC}-V_{EE}}{68\k\Omega}
$$

En el caso de una ESP32 típicamente:

$$
V_{CC}=3.3V,\qquad V_{EE}=0V
$$

Entonces:

$$
I=\frac{3.3}{68000}
$$

Resultado numérico

$$
I_{max}=0.0000485\ A
$$

Conversión a miliamperios:

$$
I_{max}=0.0000485 \times 1000
$$

$$
I_{max}=0.0485\ mA
$$

Este valor es considerablemente menor que el límite de seguridad de **1 mA** establecido para este tipo de aplicaciones biomédicas. Por lo tanto, incluso en el caso extremo en el que la resistencia de la piel sea muy baja, el circuito diseñado garantiza que la corriente que atraviesa al usuario permanece dentro de rangos seguros.

Esto demuestra que la resistencia limitadora de **68 kΩ** cumple adecuadamente su función de restringir la corriente en el sistema, permitiendo realizar la medición de la conductancia cutánea sin representar un riesgo para el usuario.

## Diseño del circuito de medición GSR

El circuito implementado para la medición de la respuesta galvánica cutánea se basa en un divisor resistivo, en el cual la resistencia de la piel del usuario forma parte del circuito eléctrico. La señal es capturada mediante dos electrodos colocados sobre la piel, generalmente en los dedos o la palma de la mano, regiones que presentan una alta densidad de glándulas sudoríparas y permiten obtener variaciones más sensibles de la conductancia cutánea.

En el circuito, los electrodos se conectan a una fuente de alimentación positiva (V+), mientras que el nodo de medición se conecta al pin analógico A0 del Arduino. Desde este punto se conecta una resistencia R1 de 68 kΩ hacia tierra, formando así el divisor resistivo. Las variaciones en la resistencia de la piel producen cambios en el voltaje presente en el nodo de medición, los cuales son detectados por el conversor analógico-digital (ADC) del microcontrolador.

Adicionalmente, el circuito incorpora un condensador C1 de 1 µF conectado en paralelo con la resistencia. Este condensador actúa como un filtro pasa-bajos que permite reducir el ruido de alta frecuencia y estabilizar la señal adquirida, mejorando la calidad de la medición.

Cuando la actividad del sistema nervioso simpático aumenta, se incrementa la actividad de las glándulas sudoríparas, lo que reduce la resistencia eléctrica de la piel y aumenta su conductancia. Como consecuencia, el voltaje medido en el nodo analógico del Arduino cambia, permitiendo registrar las variaciones de la señal GSR en tiempo real para su posterior visualización y análisis.

El uso de una resistencia de 68 kΩ garantiza que la corriente que circula a través del cuerpo sea extremadamente baja, manteniéndose muy por debajo del límite de seguridad de 1 mA, lo cual asegura condiciones seguras para el usuario durante la medición.

<img width="420" height="248" alt="image" src="https://github.com/user-attachments/assets/d7f8e9eb-e917-49b3-a7f8-72f55f33d52d" />

