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
El sistema propuesto para la medición de la respuesta galvánica cutánea se alimenta con un funete de voltaje baja, entre 3.3 y 5 v. Debido a que el dispositivo entra en contacto directo con el cuerpo humano, es de vital importancia garantizar que la corriente que circule a través de la piel del usuario se mantenga dentro de límites seguros.
Para verificar que el circuito es seguro, se calcula la corriente que podría circular por el usuario. En el circuito, la corriente queda limitada por la resistencia R1 = 68 kΩ y por la resistencia de la piel 
 R_{\text{piel}.La ecuación general es:
 $$
 $I=\frac{V_{CC}-V_{EE}}{68\,k\Omega + R_{\text{piel}}}$.
 $$
Para seguridad se analiza el caso extremo:

 R_{\text{piel}: 0
 
Sustituyendo:

 $I=\frac{V_{CC}-V_{EE}}{68\,k\Omega}$.​

En ESP32 típicamente:

V_{CC} = 3.3 V, V_{EE} = 0 V

Entonces:
