# Actividad 1: Orientación y primer vistazo al entorno gráfico

1. Incluye una captura de pantalla del ejemplo funcionando en tu máquina.
R//: 
<img width="1912" height="1016" alt="image" src="https://github.com/user-attachments/assets/d7d45695-235d-4741-bd56-cafc3c868a2f" />

3. ¿Qué preguntas te surgen al ver el código? Anota al menos tres preguntas que te gustaría investigar más adelante (no te preocupes que la idea de esta unidad es que las resuelvas).
R//:
1. ¿que es un VAO/VBO?
2. ¿para que sirve el GLFW?
3. ¿los shaders no se utilizan de forma mas compleja?

# Actividad 2: ¿Cómo se crea un proyecto OpenGL en Windows?
Para que un proyecto OpenGL funcione en Windows se utilizan varias bibliotecas que trabajan juntas, GLFW sirve para crear la ventana del programa y manejar el teclado y el mouse. También permite crear el contexto de OpenGL, que es necesario para poder dibujar gráficos. Por otro lado, está opengl32.lib, que viene con Windows y permite enlazar el programa con las funciones de OpenGL. sin embargo, esta biblioteca solo incluye funciones hasta OpenGL 1.1, para eso se utiliza GLAD, que se encarga de cargar las funciones más modernas de OpenGL de los drivers de la tarjeta gráfica. Los drivers de la GPU son los que permiten que el programa se comunique con la tarjeta gráfica para procesar y mostrar los gráficos. Finalmente, GLM es una biblioteca que sirve para trabajar con vectores, matrices y transformaciones, lo cual facilita los movimientos y efectos en objetos en 3D.todas estas herramientas se complementan: GLFW crea la ventana y prepara el contexto, opengl32.lib permite enlazar las funciones básicas, GLAD carga las funciones modernas que ofrecen los drivers de la GPU y GLM ayuda con los cálculos matemáticos. Al configurar correctamente todas las dependencias en Visual Studio, podemos compilar y ejecutar nuestro programa OpenGL.

# Actividad 3: 
Qué tal si ensayas. Prueba con esta línea

`// 9) Configura el viewportglViewport(0, 0, bufferWidth, bufferHeight);`
¿Qué pasa si?

`glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);`
Cambia los valores de bufferWidth y bufferHeight: divide por 2, por 4, multiplica por 2, por 4, etc. ¿Qué pasa? ¿Qué observas? ¿Qué crees que está pasando?
R//: al dividir por 2 la imagen se aleja del triangulo y lo deja en la esquina inferior izquierda, al dividir por 4 la imagen se aleja aun mas y el triangulo se ve mas pequeño todavia.

al multiplicar por 2 se acerca la imagen y hace mas grande el triangulo, todo lo contrario a lo anterior y se enfoca en la esquina izquierda del triangulo y se muestra como si se hiciera zoom, al multiplicar por 4 se acerca tanto que el triangulo desaparece y se ve solo el fondo

Ya llevas un rato leyendo y no has hecho digestión. Para favorecer tu aprendizaje, es necesario que te detengas un momento y ELABORES lo que has visto hasta ahora. Mira, quiero contarte algo. Lo que he venido haciendo de manera implícita en el curso es enseñarte a aprender a aprender. ¿Te has dado cuenta? Te voy exponiendo a conceptos y luego te pido que experimentes, que los pongas en práctica, que los reflexiones. Entonces, no te quedes largos periodos de tiempo leyendo, viendo tutoriales o escuchando. Cada cierto tiempo, puede ser cada 30 minutos o cada hora, haz una pausa y reflexiona sobre lo que has aprendido.
¿Cómo lo haces? Realiza un resumen de lo que has aprendido hasta ahora, haciendo un diagrama conceptual o un mapa mental. Experimentando. ¿Cómo? Haciendo la pregunta mágica: ¿Qué pasaría si? ¿Qué pasaría si cambio el tamaño de la ventana? ¿Qué pasaría si cambio el tamaño del viewport?
Entonces hagamos “digestión”: en tu bitácora, escribe un resumen de lo que has aprendido hasta ahora y piensa en un experimento del tipo ¿Qué pasaría si?

R//: Entendí que el contexto OpenGL es el entorno donde se guardan los recursos y estados necesarios para dibujar gráficos, como texturas, shaders y buffers. GLFW se encarga de crear la ventana y el contexto, mientras que OpenGL envía las instrucciones y la GPU las ejecuta para dibujar en el framebuffer, que es como una hoja donde se forma la imagen antes de mostrarse en pantalla. También aprendí que el viewport define el área donde se dibuja y que debe ajustarse cuando cambia el tamaño de la ventana.

mi experimento seria que usando la actividad anterior de multiplicar y dividir en glViewport(0, 0, bufferWidth, bufferHeight); que pasaria si multiplico en un y divido en otro por ejemplo: glViewport(0, 0, bufferWidth/2, bufferHeight*2); multiplico la altura por 2 y el ancho lo divido por 2.

Resultado: esta atrocidad...
<img width="1915" height="1015" alt="image" src="https://github.com/user-attachments/assets/f7b8e3f6-314c-4ad1-87a9-d933498836b2" />

¿Qué pasa si cambias el primer parámetro de glDrawArrays a GL_LINES? 
R//: se dibuja una linea en vez de un triangulo.

¿Qué pasa si lo cambias a GL_POINTS? 
R//: se crea un punto diminuto en la pantalla 

¿Qué pasa si cambias el tercer parámetro a 2? 
R//: lo intente con el triangulo y desapareció de la imagen y no se mostró nada

¿Qué pasa si lo cambias a 4?
R//: se muestra otra vez el triangulo como si nada

¿Qué es el contexto OpenGL?
R//: Es el entorno que permite utilizar OpenGL y administrar sus estados, recursos y operaciones gráficas para dibujar en pantalla.

¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?
R//: GLFW puede crear ventanas, gestionar entradas del teclado y mouse, y crear el contexto OpenGL. de ventaja tiene que facilita estas tareas y permite trabajar con gráficos sin programar todo desde cero.

¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?
R//: Porque necesita un espacio de trabajo con herramientas y recursos para dibujar, el contexto proporciona el entorno donde se realizan las operaciones gráficas.

¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?
R//: Es la memoria donde se almacena la imagen que se va a mostrar y se puede relacionar con los píxeles y como se ven las imagenes como en las unidades 1 y 2.

¿Qué relación hay entre el viewport y el framebuffer?
R//: El framebuffer almacena la imagen, mientras que el viewport define el área de la ventana donde OpenGL transforma y dibuja las coordenadas de los objetos.

¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?
R//: Los drivers permiten que OpenGL se comunique con la tarjeta gráfica. La GPU procesa las operaciones gráficas y ejecuta los shaders para generar la imagen.

¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?
R//: VSync sincroniza los cuadros generados con la frecuencia de actualización del monitor, evitando que la imagen se vea dividida (lo que se conoce como tearing), sin VSync una imagen estática probablemente se verá normal, pero una imagen dinámica puede presentar cortes y consumir más recursos al generar cuadros innecesarios.

En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?
R//: OpenGL Legacy es el estilo antiguo que permite utilizar funciones como glBegin() y glEnd() para dibujar directamente. OpenGL moderno utiliza shaders, VAO y VBO, dando mayor control y eficiencia sobre el procesamiento gráfico.

¿Qué es el shader program? ¿Por qué es importante en OpenGL moderno?
R//: Es un programa que reúne los shaders compilados y enlazados, como el vertex shader y el fragment shader, es importante porque define cómo se procesan los vértices y qué color tendrán los píxeles.

Trata de revisar el código setupTriangle(), intuitivamente ¿Qué crees que hace? ¿Qué crees que es el VAO y el VBO?
R//: La función crea los datos de los tres vértices del triángulo y configura los recursos necesarios para dibujarlo.
- VBO: almacena los datos de los vértices en la memoria de la GPU.
- VAO: guarda la configuración de cómo OpenGL interpreta esos datos y los atributos de los vértices.

En el ciclo principal (game loop) de OpenGL, notaste que en cada frame (cuadro) le decimos a openGL que use el shader program y el VAO. Si le indicas esto antes del game loop ¿Será necesario seguirlo haciendo en cada loop? Si no es necesario ¿En qué casos crees que esto puede ser útil?
R//: Sí, si se necesita asegurar que estén activos en cada dibujo, porque otros objetos o procesos pueden cambiar el estado de OpenGL, si nada cambia ese estado, no siempre es necesario repetir las instrucciones. Es útil hacerlo cuando se dibujan diferentes objetos que utilizan distintos shaders o VAO.

Finalmente, recuerda lo que hace glfwSwapBuffers(mainWindow); ¿Por qué crees que es importante? ¿Qué pasaría si no lo llamas? ¿Cómo explicas lo que pasa si no lo llamas? (experimenta)
R//: Intercambia el buffer trasero, donde se dibuja el triángulo, con el buffer delantero, que se muestra en pantalla. Si no se llama, los cambios podrían no aparecer y la ventana podría quedarse mostrando una imagen anterior o vacía, porque el contenido dibujado no se presenta mediante el intercambio de buffers.

# Actividad 4 #

¿Cuál es la diferencia entre una CPU y una GPU para responder esta pregunta te pediré que veas el siguiente video de NVIDIA. No te asustes, es muy entretenido. Mythbusters Demo GPU versus CPU.
R//: La CPU procesa tareas generales de una mejor forma, ejecutando instrucciones complejas y secuenciales. En cambio, la GPU está diseñada para realizar muchas operaciones en paralelo, por lo que es ideal para procesar gráficos, imágenes y videojuegos.

Luego de estudiar las unidades 1 y 2 de este curso y ver el video, escribe con tus propias palabras ¿Cuál es la diferencia entre una CPU y una GPU?
R//: La CPU está diseñada para realizar tareas generales y procesar instrucciones complejas de forma rápida, mientras que la GPU está diseñada para ejecutar muchas operaciones en paralelo.

¿Cuáles son los tres pasos claves del pipeline de OpenGL? Explica en tus propias palabras cuál es el objetivo de cada paso.
R//: Procesamiento geométrico: procesa los vértices y determina la posición de los objetos.
Rasterización: convierte las figuras en fragmentos que corresponden a las zonas que ocupan en la pantalla.
Procesamiento de fragmentos: calcula el color final y determina qué partes se muestran en la imagen.

La gran novedad que introduce OpenGL moderno es el pipeline programable. ¿Qué significa esto? ¿Qué diferencia hay entre el pipeline fijo y el programable? ¿Qué ventajas le ves a esto? y si el pipeline es programable, ¿Qué tengo que programar?
R//: El pipeline programable permite escribir shaders para controlar cómo se procesan los vértices y los fragmentos. El pipeline fijo utiliza operaciones predefinidas que ofrecen menos libertad. Su ventaja es que podemos crear efectos, colores e iluminación personalizados. Debemos programar los shaders, principalmente el vertex shader y el fragment shader.

Si fueras a describir el proceso de rasterización ¿Qué dirías?
R//: Es el proceso que convierte figuras geométricas, como triángulos, en fragmentos que representan las partes que ocupan en la pantalla.

¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un pixel? ¿Por qué?
R//: Los fragmentos contienen información como la posición, el color y la profundidad de una parte de una figura. No son necesariamente iguales a los píxeles, porque un fragmento es un candidato a generar o modificar un píxel, pero puede descartarse durante el procesamiento.

Explica qué problema resuelve el Z-buffer y ¿Qué es el depth test?
R//: El Z-buffer almacena información sobre la profundidad de los elementos dibujados. El depth test compara la profundidad de un fragmento con la que ya está almacenada para determinar si debe mostrarse o quedar oculto detrás de otro objeto.

¿Por qué se presenta el problema de la aliasing? ¿Qué es el anti-aliasing?
R//: El aliasing ocurre porque la pantalla está formada por píxeles y las líneas diagonales o curvas pueden verse dentadas. El anti-aliasing reduce ese efecto suavizando los bordes de las figuras.

¿Qué relación hay entre la iluminación y el fragment shader? Siempre es necesario tener en cuenta la iluminación en un fragment shader? o puedo hacer un fragment shader sin iluminación? Explica que implicaciones tiene esto.
R//: El fragment shader puede calcular la iluminación para determinar cómo se ve una superficie. Sin embargo, no es obligatorio utilizarla: podemos asignar directamente un color. Sin iluminación, los objetos pueden verse planos, pero el procesamiento es más sencillo.

¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?
R//: La GPU debe realizar más cálculos por cada fragmento para determinar cómo afecta cada luz al objeto. Esto puede aumentar el consumo de recursos y reducir el rendimiento, especialmente si hay muchas luces y superficies que procesar.

Escribe un resumen en tus propias palabras de lo que se necesita para dibujar un triángulo en OpenGL.
R//:
   
Escribe un resumen en tus propias palabras de lo que necesitas para poder usar un shader en OpenGL.
R//:

Implementa el código anterior en tu máquina y captura pantalla del resultado. Pero antes de hacerlo trata de predecir qué va a pasar.
R//: 

# Actividad 5 #

Modifica el código del triángulo para que sea interactivo.
R//:

Incluye una captura de pantalla del triángulo interactivo funcionando en tu máquina.
R//:

Explica el proceso de normalización de las coordenadas del mouse y cómo se relaciona con el sistema de coordenadas de OpenGL.
R//:

Explica el proceso de normalización a coordenadas de dispositivo (NDC) y cómo se relaciona con el sistema de coordenadas de OpenGL.
R//:

# Actividad 6 #

