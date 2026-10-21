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
R//:  
