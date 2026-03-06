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
I=\frac{V_{CC}-V_{EE}}{68\,k\Omega + R_{\text{piel}}}
$$

Para verificar la seguridad del circuito se analiza el caso extremo:

$$
R_{\text{piel}} = 0
$$

Sustituyendo en la ecuación:

$$
I=\frac{V_{CC}-V_{EE}}{68\,k\Omega}
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

# Diseño del dispositivo vestible

El dispositivo vestible desarrollado para la medición de la respuesta galvánica cutánea se diseñó con el objetivo de permitir la captura de la señal de conductancia de la piel de forma sencilla y portátil. Para la adquisición de la señal se utilizaron tiras de aluminio colocadas en los dedos del usuario, las cuales funcionan como electrodos encargados de detectar las variaciones en la conductancia eléctrica de la piel. Estas tiras se conectan mediante cables al circuito implementado en una protoboard.

En la protoboard se encuentran los componentes electrónicos del sistema, incluyendo la resistencia de 68 kΩ y el condensador utilizados para el acondicionamiento de la señal, así como el microcontrolador ESP32 encargado de la adquisición y transmisión de los datos. Con el fin de que el sistema pudiera utilizarse como un dispositivo vestible, la protoboard junto con el ESP32 se colocó en la muñeca del usuario y se fijó utilizando cintas de velcro.

La alimentación del sistema se realizó mediante una power bank, lo que permite que el dispositivo funcione de manera portátil sin necesidad de una conexión directa a un computador. Debido a que la transmisión de datos debía realizarse de forma inalámbrica, se empleó la conectividad Bluetooth del ESP32 para enviar la información capturada hacia el computador, donde posteriormente se visualiza y analiza la señal obtenida.

# Implementación del sistema

## Programación del microcontrolador

El código implementado en el microcontrolador ESP32 permite adquirir la señal proveniente del circuito de medición de conductancia cutánea y transmitirla de forma inalámbrica hacia un computador mediante Bluetooth.

```bash
#include "BluetoothSerial.h"

BluetoothSerial SerialBT;

const int adcPin = 34;

const int fs = 1000;
const unsigned long Ts = 1000000/fs;

unsigned long lastSample = 0;

void setup() {

  Serial.begin(115200);

  SerialBT.begin("ESP32_EMG");

  analogReadResolution(12);
  analogSetAttenuation(ADC_11db);

  lastSample = micros();
}

void loop() {

  unsigned long now = micros();

  if (now - lastSample >= Ts) {

    lastSample += Ts;

    int adcValue = analogRead(adcPin);

    if (SerialBT.hasClient()) {
      SerialBT.println(adcValue);
    }

  }

}
```
Para ello se utiliza la librería BluetoothSerial, que habilita la comunicación inalámbrica con otros dispositivos, y se crea el objeto SerialBT para gestionar el envío de datos. La señal analógica del circuito se recibe a través del pin 34, conectado al nodo del divisor resistivo formado por la resistencia de 68 kΩ y la resistencia de la piel. El sistema se configura para trabajar con una frecuencia de muestreo de 1000 Hz, lo que permite capturar mil muestras por segundo, controlando el tiempo entre lecturas mediante la función micros(). Durante la inicialización se establecen las comunicaciones seriales y Bluetooth con el nombre “ESP32_EMG”, y se configura el convertidor analógico–digital del ESP32 con una resolución de 12 bits, lo que permite obtener valores entre 0 y 4095 y mejorar la precisión de la medición. Posteriormente, en cada ciclo del programa se realiza la lectura de la señal mediante analogRead() y, si existe un dispositivo conectado por Bluetooth, el valor adquirido se envía al computador utilizando SerialBT.println(), permitiendo visualizar y analizar la señal en tiempo real.

# Respuesta a las preguntas planteadas en la práctica:

## ¿A qué se debe que una inspiración profunda incremente la magnitud de la respuesta galvánica cutánea (GSR)?

El incremento de la magnitud de la respuesta galvánica cutánea (GSR) durante una inspiración profunda se explica principalmente por la modulación del sistema nervioso autónomo (SNA), específicamente por la activación del componente simpático, que regula la actividad de las glándulas sudoríparas ecrinas.

Durante una inspiración profunda ocurre un fenómeno conocido como acoplamiento cardiorrespiratorio o modulación respiratoria autonómica. La expansión torácica y la activación de los centros respiratorios en el bulbo raquídeo generan señales aferentes provenientes de mecanorreceptores pulmonares y receptores de estiramiento torácico que proyectan hacia estructuras del tronco encefálico y del sistema límbico, regiones que también participan en la regulación autonómica. Este proceso produce un incremento transitorio en la actividad simpática, especialmente en las fibras sudomotoras colinérgicas que inervan las glándulas sudoríparas ecrinas de la piel.

La GSR mide cambios en la conductancia eléctrica de la piel, la cual depende directamente del grado de hidratación del estrato córneo y de la actividad sudorípara. Cuando la activación simpática incrementa la secreción de sudor (incluso en cantidades microscópicas), se reduce la resistencia cutánea y aumenta la conductancia, generando una respuesta fásica conocida como Skin Conductance Response (SCR).

Además, la inspiración profunda puede actuar como un estímulo fisiológico interno que induce una respuesta de orientación o arousal autonómico, fenómeno ampliamente documentado en estudios psicofisiológicos. Este aumento del arousal produce una mayor liberación de acetilcolina en las terminales sudomotoras, aumentando temporalmente la conductancia cutánea.

## ¿Cuáles serían las ventajas y desventajas de utilizar la GSR como indicador de estrés?

La respuesta galvánica cutánea es uno de los biomarcadores psicofisiológicos más utilizados para la evaluación del nivel de activación autonómica, especialmente del componente simpático. Sin embargo, su utilización como indicador de estrés presenta tanto fortalezas metodológicas como limitaciones interpretativas.

### Ventajas

Una de las principales ventajas de la GSR es su alta sensibilidad a cambios en la activación simpática. Dado que las glándulas sudoríparas ecrinas están exclusivamente inervadas por fibras simpáticas sudomotoras, la conductancia cutánea refleja de forma directa la actividad de este sistema, permitiendo detectar variaciones rápidas en el estado de activación fisiológica.

Otra ventaja importante es que se trata de una técnica no invasiva, de bajo costo y fácil implementación, lo que facilita su uso en estudios experimentales, entornos clínicos y aplicaciones de monitoreo continuo. Además, la GSR posee una alta resolución temporal, permitiendo identificar respuestas fásicas asociadas a estímulos específicos, lo que resulta útil para analizar la reactividad emocional o cognitiva frente a eventos particulares.

Asimismo, la señal puede ser procesada para separar componentes tónicos (Skin Conductance Level, SCL) y fásicos (SCR), lo cual permite evaluar tanto el nivel basal de activación autonómica como las respuestas transitorias ante estímulos estresores.

### Desventajas

A pesar de su sensibilidad, una limitación fundamental de la GSR es su baja especificidad. La conductancia cutánea no es un marcador exclusivo de estrés, sino que refleja cualquier tipo de activación fisiológica o emocional, incluyendo excitación, atención, sorpresa, actividad cognitiva o cambios térmicos. Por lo tanto, un aumento en la GSR no necesariamente implica la presencia de estrés.

Otra desventaja relevante es su alta susceptibilidad a factores externos y fisiológicos. Variables como la temperatura ambiente, la humedad, el movimiento, el contacto de los electrodos, la hidratación de la piel o la actividad física pueden alterar significativamente la señal, introduciendo artefactos o variabilidad interindividual.

También existe una variabilidad considerable entre sujetos, debido a diferencias en la densidad de glándulas sudoríparas, características de la piel y estado fisiológico basal, lo que dificulta la comparación directa entre individuos sin un proceso adecuado de normalización o calibración.

Finalmente, la GSR presenta una latencia relativamente lenta en comparación con otros indicadores fisiológicos, ya que las respuestas sudomotoras suelen aparecer entre 1 y 3 segundos después del estímulo, lo que puede limitar su precisión temporal en ciertos paradigmas experimentales.

# Referencias:
-Phadke, A. N., Harasheh, K., & Gill, S. (2026). Wearable IoT-enabled galvanic skin response device for objective pain and stress monitoring. Sensors, 26(1), 116. https://doi.org/10.3390/s26010116

- Arsalan, A., Majid, M., Anwar, S. M., & Khan, M. (2022). Human stress assessment: A comprehensive review of methods using wearable sensors. IEEE Access, 10, 39373–39389.

- Al-Nafjan, A., & Aldayel, M. (2024). Anxiety detection system based on galvanic skin response signals. Applied Sciences, 14(23), 10788. https://doi.org/10.3390/app142310788

- Cowley, B., & Torniainen, J. (2016). A short review and primer on electrodermal activity in human-computer interaction applications. Foundations and Trends in Human-Computer Interaction, 9(1), 1–46.

- Guzik, P., et al. (2021). Correlation analysis of different measurement places of galvanic skin response. Sensors, 21(12), 4210. https://doi.org/10.3390/s21124210

- Pop-Jordanova, N., et al. (2020). Electrodermal activity and stress assessment. Prilozi, 41(2), 5–15. https://doi.org/10.2478/prilozi-2020-0028

- Webster, J. G. (2010). Medical instrumentation: Application and design (4th ed.). Wiley.
