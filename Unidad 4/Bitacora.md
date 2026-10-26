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

