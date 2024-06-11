# ¿Otra vez un chat?

## Introducción

La Inteligencia Artificial generativa ha generado un gran entusiasmo y expectativas. Sin embargo, cuando se trata de implementarla en procesos concretos, este entusiasmo a menudo da paso al escepticismo. "¿Otra vez un chat?" es una reacción común que refleja la confusión y la frustración alrededor de cómo incorporar estas tecnologías de manera efectiva. Esta respuesta es comprensible dado la complejidad y la falta de claridad sobre cómo la IA puede integrarse en las operaciones diarias de una empresa.

Pero lo que muchos pasan por alto es que un chat es solo la punta del iceberg. Es una interfaz, un mecanismo de comunicación entre la IA y el humano, pero no es la IA en sí misma. Detrás de esta interfaz, se esconde un mundo de posibilidades y complejidades que vale la pena explorar.

Desde los fundamentos de los modelos de lenguaje, que pueden generar texto coherente a partir de una simple predicción de palabras, hasta técnicas como el prompt engineering y el aprendizaje en contexto, que nos permiten adaptar estos modelos a nuestras necesidades específicas. Pasando por arquitecturas más complejas como el Retrieval Augmented Generation (RAG) y los agentes conversacionales, que expanden las capacidades de la IA generativa hacia la ampliación del conocimiento, la toma de decisiones y la ejecución de acciones autónomas.

Pero quizás lo más importante es comprender cómo todo estas complejidades tienen un único objetivo: aumentar nuestro control sobre la IA. Porque al final del día, lo que buscamos es una herramienta que pueda entender nuestras intenciones y generar resultados alineados con nuestros objetivos.

Y es desde esta mirada que los modelos multimodales prometen llevar esta interacción humano-IA a nuevas posibilidades, permitiéndonos comunicarnos de formas más naturales e intuitivas.

Así que sí, vamos a hablar, por ahora, otra vez de un chat.

## El perro... El perro ladra... El perro ladra fuerte...

En el corazón de los modelos de lenguaje como GPT, se encuentra una tarea en apariencia sencilla: predecir la siguiente palabra en una secuencia. Introduce "El" y el modelo generará "perro". Luego, "El perro" se convierte en el input para predecir la siguiente palabra, digamos "ladra". A continuación, "El perro ladra" se usa para generar "fuerte". Y así sucesivamente, en un proceso autoregresivo que puede continuar indefinidamente.

Puede parecer un juego trivial, pero aquí está lo increíble: a partir de esta simple tarea, los modelos de lenguaje han desarrollado habilidades asombrosas. Pueden generar textos coherentes, responder preguntas, resumir información, traducir idiomas e incluso escribir código. Y todo esto sin haber sido entrenados explícitamente para estas tareas. Es como si al aprender a predecir palabras, hubieran absorbido una comprensión profunda del lenguaje y sus múltiples usos.

## Prompts por doquier

Para aprovechar al máximo este potencial, se utiliza el "prompt engineering", que consiste en estructurar cuidadosamente los inputs para guiar la generación de texto hacia el resultado deseado. Por ejemplo, para obtener un resumen, se podría indicar: "Resume el siguiente texto: [insertar texto]". El modelo generará un resumen conciso y bien estructurado. Así mismo, se puede solicitar que el texto se genere con un estilo particular, como el de un autor reconocido, simplemente incluyendo esta instrucción en el prompt.

## Aprendiendo del contexto

Una de las características más notables de los modelos de lenguaje es su capacidad de aprender en contexto, es decir, aprovechar ejemplos proporcionados para mejorar la exactitud y presición de su respuesta. Por ejemplo, para generar descripciones de productos, se pueden proporcionar algunos ejemplos y el modelo identificará los patrones para generar descripciones similares para nuevos productos, sin necesidad de ajustar el modelo de lenguaje.

Esta capacidad de aprendizaje en contexto permite a los modelos de lenguaje adaptarse rápidamente a dominios específicos y a las necesidades particulares de cada organización, sin requerir un entrenamiento extensivo y costoso. Basta con proporcionar unos pocos ejemplos relevantes dentro del prompt para que el modelo "aprenda" sobre la marcha y genere resultados adaptados al contexto.

## Mejorando el contexto con RAG

A medida que las tareas se complejizan, surge la necesidad de que el modelo acceda a información adicional para generar respuestas más exactas y precisas. Aquí entra en juego el Retrieval Augmented Generation (RAG). Con RAG, el modelo no solo se basa en el prompt y su conocimiento previo, sino que también puede buscar y utilizar información relevante de una base de conocimientos de la organización.

Imaginemos que tenemos una gran cantidad de documentación interna en nuestra empresa. Podemos convertir esta información en embeddings, un formato comprensible para el modelo. Cuando un usuario hace una pregunta, el modelo busca en estos embeddings la información más relevante y la incluye en el contexto para generar una respuesta de acuerdo a dicha información. Es como tener un bibliotecario experto que rápidamente encuentra el libro adecuado para responder a nuestra consulta.

RAG amplía enormemente las capacidades de los modelos de lenguaje, permitiéndoles acceder a conocimientos específicos de un dominio o una organización. Ya no están limitados a su conocimiento previo, sino que pueden aprovechar toda la riqueza de información disponible en nuestras bases de datos y documentos.

## Memoria y conversación

Una característica clave de los sistemas de chat basados en modelos de lenguaje es su capacidad para mantener el contexto de la conversación. A medida que interactuamos con el modelo, este va acumulando la historia de nuestro diálogo, permitiendo respuestas más coherentes y relevantes.

Esta memoria conversacional transforma la interacción de un simple intercambio de preguntas y respuestas a una conversación fluida y contextualizada. El modelo puede hacer referencia a aspectos mencionados anteriormente, pedir aclaraciones y construir sobre ideas previas. Es como tener una discusión con un colega que recuerda perfectamente todo lo que se ha dicho y puede hilvanar los diferentes hilos de la conversación.

Esta capacidad de mantener el contexto es especialmente poderosa cuando se combina con técnicas como RAG. El modelo no solo puede acceder a información relevante para la consulta actual, sino que también puede considerar el contexto de la conversación para ofrecer respuestas aún más precisas y personalizadas.

## Que decida el agente

Los sistemas de chat basados en modelos de lenguaje permiten una interacción natural con la IA, manteniendo el contexto de la conversación para brindar respuestas coherentes. Pero los agentes van más allá: pueden tomar decisiones, realizar acciones y aprender de los resultados.

Imaginemos un escenario en el que un cliente plantea un problema a través del chat. Un agente podría analizar la consulta, determinar los pasos necesarios para resolverla, ejecutar esas acciones interactuando con diferentes sistemas y bases de datos, y luego evaluar la efectividad de la solución propuesta. Todo esto sin requerir instrucciones explícitas del usuario en cada paso.

Esto nos acerca a una interacción fluida y proactiva con la IA, donde podemos expresar nuestras necesidades en lenguaje natural y confiar en que el agente encontrará la mejor manera de ayudarnos. Es como tener un asistente experto que no solo nos escucha, sino que también piensa por sí mismo y trabaja diligentemente para resolver nuestros problemas.

## El control como objetivo central

A lo largo de todas estas innovaciones, un objetivo central se mantiene constante: el control. Desde las técnicas de prompt engineering hasta los agentes conversacionales, cada capa de complejidad que añadimos a los modelos de lenguaje tiene como objetivo final incrementar nuestro control sobre la salida generada.

Ya sea proporcionando instrucciones claras, ejemplos en contexto, información externa a través de RAG, o dotando a los modelos con habilidades de toma de decisiones, siempre buscamos formas de guiar la generación de texto hacia nuestros objetivos específicos.

Mientras los modelos de lenguaje no puedan leer directamente nuestros pensamientos, seguiremos buscando estrategias innovadoras para proporcionarles más contexto, más ejemplos, más información externa, y así lograr un mayor control sobre su generación.

## El futuro es multimodal

Mirando hacia el futuro, los modelos multimodales prometen llevar nuestra interacción con la IA generativa a nuevas alturas. Estos modelos, capaces de entender y generar no solo texto, sino también imágenes y audio, nos permitirán comunicarnos con la IA de formas más naturales e intuitivas.

Imagina un modelo de IA integrado en nuestro equipo de trabajo, entrenándose continuamente con nuestra información, sin necesidad de salir de nuestro entorno. Un modelo que no solo comprende nuestras palabras, sino también las imágenes que compartimos y el tono de nuestra voz. Un asistente que está siempre escuchando en el fondo, generando acciones a medida que va comprendiendo nuestros objetivos.

Esta interacción multimodal provee al modelo con una riqueza de información sin precedentes. Ya no tenemos que redactar laboriosamente un mensaje en el chat, sino que podemos conversar naturalmente, compartir pantallas, dibujar diagramas, todo en una misma interfaz. Cuanta más información contextual reciba el modelo, mejor podrá comprender nuestras intenciones y generar mojores respuestas.

Y así, cuando alguien pregunte "¿otra vez un chat?", podremos responder con confianza: "Realmente es mucho más que un chat. Esto es una interfaz multidimensional para colaborar con una IA que entiende y genera contenido en múltiples modalidades. Una IA que podemos controlar y adaptar a nuestras necesidades con una precisión sin precedentes. Esto, amigos míos, es el futuro de la interacción humano-IA."

Y así, cuando alguien pregunte "¿Me vas a hablar de un chat?", podremos responder con confianza: "No, no se trata solo de un chat. Hablamos de una interfaz para interactuar con una IA capaz de entender y generar contenido en multimodal. Hablamos de cómo podemos controlar y adaptar esta IA a nuestras necesidades específicas. Hablamos de cómo mejorar y hacer más fluida la interacción entre humanos e IA."