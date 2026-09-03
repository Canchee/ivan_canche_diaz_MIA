# Ejercicio 2 — Descripción PEAS de agentes inteligentes

## Contexto

En el capítulo 2 de *Artificial Intelligence: A Modern Approach* (Russell & Norvig),
un agente se entiende mejor cuando se especifica su **entorno de tarea**. Una forma
estándar de hacerlo es la descripción **PEAS**:

| Letra | Significado | Pregunta guía |
|---|---|---|
| **P** | *Performance* (medida de desempeño) | ¿Cómo se evalúa el éxito del agente? |
| **E** | *Environment* (entorno) | ¿En qué mundo opera? ¿Quién más actúa ahí? |
| **A** | *Actuators* (actuadores) | ¿Qué acciones puede ejecutar? |
| **S** | *Sensors* (sensores) | ¿Qué información puede percibir? |

Este ejercicio **no requiere programar**. Consiste en analizar distintos tipos de
aplicaciones reales y describir cada una con el esquema PEAS.

## Objetivo

Para cada una de las **8 aplicaciones** listadas abajo, redacta una descripción
PEAS completa y coherente. Debes pensar como diseñador del agente: qué optimiza,
dónde actúa, con qué puede mover o modificar el mundo, y qué puede observar.

## Aplicaciones a analizar

### Asistente virtual de voz

- **Performance:** Logra activarse por el comando determinado, entender el request del usuario, analizar y ejecutar la acción que el usuario solicitó.

- **Environment:** Habitaciones; el dispositivo puede encontrarse en un hogar, una escuela, una habitación de hotel. Automóvil; autos modernos con asistentes incluidos en su sistema de audio. En calles; lentes nuevos incluyen asistentes virtuales. Casi cualquier lugar donde una persona se encuentre en su día cotidiano puede considerarse su ambiente ya que podemos encontrar asistentes en teléfonos, relojes, televisores, autos, lentes, tablets, y en sistemas especializados.

- **Actuators:** Encender televisor, reproducir una canción, serie o película. Hacer una búsqueda por internet. Agendar una cita en calendario. Comenzar un temporizador. Monitoreo de signos vitales.

- **Sensors:** Micrófono, cámara, sensor de temperatura, sensor de oxígeno en la sangre, horario.

### Robot aspirador doméstico

- **Performance:** Completar un recorrido a través de la superficie sobre la cual se encuentra. Detectar y evitar obstáculos, así como evitar caerse por escaleras o lugares que se encuentren debajo de la superficie colocada. Avisar al usuario que su recorrido terminó e informar del tiempo que le tomó completar dicho recorrido.

- **Environment:** Superficie que incluye obstáculos, escaleras, personas, mascotas. El robot aspiradora debe limpiar la superficie y terminar su recorrido a pesar los obstáculos que encuentre.

- **Actuators:** Motores para mover el robot y darle dirección. Motor de aspiradora que se encarga de aspirar la suciedad que se encuentre en su trayectoria y que debe detenerse al concluir el recorrido.

- **Sensors:** Sensores para detectar obstáculos y superficies que representen peligro de caída. Cámara, algunos robot aspiradora modernos incluyen cámaras para videovigilancia y monitoreo. Sensor de nivel de batería.

### Sistema de recomendación de streaming

- **Performance:** Recomendar películas o series de acuerdo al historial del usuario y de los beneficios económicos de la plataforma de streaming. Su performance puede evaluarse en la cantidad de clics que realiza el usuario a las recomendaciones y relacionarlo con la retención de clientes/usuarios.

- **Environment:** Plataforma de streaming con un catálogo de series y películas.

- **Actuators:** Generar lista de películas y series. Enviar notificaciones al usuario.

- **Sensors:** Historial del usuario. Clicks que el usuario realiza a la lista de recomendaciones. Tiempo de streaming sobre las series y películas recomendadas.

### Vehículo autónomo en ciudad

- **Performance:** Llegar al destino respetando los señalamientos de la ciudad y siguiendo el reglamento de tránsito. Evitar accidentes para el usuario y las personas que se encuentren en su ambiente. Tomar la mejor ruta posible para optimizar tiempo y batería,

- **Environment:** Calles, ciudad o carretera. Señales de tránsito. Otros conductores y peatones. Obstáculos imprevistos que puedan causar algún tipo de accidente o afectación al usuario y a otras personas.

- **Actuators:** Motor para avanzar o detenerse en algún lugar. Volante para darle dirección al vehículo. Claxon para prevenir accidentes o mandar una alerta. Enviar ubicación al usuario y mostrar la ruta o trayecto planeado. Encender luces para hacer cambio de carriles. Encender faros al detectar poca iluminación, ya sea por el horario, clima o entrar a un ambiente oscuro.

- **Sensors:** ADAS; sistemas de asistencia al conductor para detectar otros automóviles y peatones, esto incluye cámaras, sensores de proximidad, sensores infrarrojos, GPS. Sensores de luz solar. Sensores de temperatura del auto. Sensores para la batería del auto.

### Agente de trading algorítmico en bolsa

- **Performance:** Tasa de ganancia positiva. Optimizar la ganancia del usuario al evitar pérdidas significativas y obtener ganancias que beneficien al usuario. Respuesta rápida ante los cambios en las tendencias de la bolsa.

- **Environment:** Bolsa de valores. Con información de los cambios en el valor de las acciones de las compañías que se encuentran en la bolsa. Modelos matemáticos de predicción o tendencias.

- **Actuators:** Comprar y vender acciones. Enviar notificaciones al usuario. Desplegar el historial de acciones.

- **Sensors:** Parámetros establecidos por el usuario para establecer márgenes de ganancia y pérdidas. Información en tiempo real del precio de las acciones.

### Sistema de diagnóstico médico asistido por IA

- **Performance:** Realizar diagnósticos precisos con los síntomas del usuario y el historial médico del usuario, así como con el apoyo de información médica. Detección temprana de enfermedades que son difíciles de detectar por el ser humano.

- **Environment:** Hospitales, clínicas, laboratorios, personal que realiza servicios en comunidades alejadas de las grandes ciudades.

- **Actuators:** Generar un diagnóstico médico. Generar recomendaciones a los médicos.

- **Sensors:** Historial médico. Síntomas del paciente. Signos vitales del paciente. Estudios realizados por laboratorio. Tomografías, electrocardiogramas, radiografías y otras herramientas que apoyen al estudio de los síntomas del paciente y provean de datos puntuales al sistema.

### Dron de inspección de infraestructura

- **Performance:** Realizar recorrido establecido y completar inspecciones a las estructuras para detectar fallas o problemas estructurales. Debe evitar obstáculos y regresar a su punto de inicio al completar su trayectoria o antes de terminar su batería.

- **Environment:** Estructuras de gran tamaño como edificios, puentes, casas o torres. Se encuentra volando así que entran factores como el clima, viento y vida salvaje como aves que lo detecten como alguna amenaza.

- **Actuators:** Motores para mover el dron en todas las direcciones. Envío de imágenes y audio. Movimiento de cámaras.

- **Sensors:** Cámaras para visualizar el espacio que se inspecciona. Cámaras específicas para la inspección de estructuras, como cámaras térmicas o infrarrojas. Sensor de batería. Giroscopio. Sensores de proximidad. GPS.

### Agente jugador de ajedrez

- **Performance:** Realizar jugadas que lleven a la victoria del agente. Capturar las piezas del adversario y evitar que tomen sus piezas. Porcentaje elevado de victorias.

- **Environment:** Un juego de ajedrez donde se encuentran las piezas del agente y del adversario. Reglas de juego y jugadas conocidas para contrarrestar movimientos del adversario.

- **Actuators:** Mover las piezas. Capturar piezas del adversario.

- **Sensors:** Método para saber el lugar de las piezas. Ya sea a través de cámara, o con vectores a que se obtengan sobre la posición de las piezas.
