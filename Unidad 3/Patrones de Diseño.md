# Actividad #8 #

1. ¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.
R//: cambie las teclas por efectos practicos a w,a,s,d: la s (Stop) detiene las particulas y las deja en la posicion donde estan, la a (Attract) dirige todas las particulas hacia el puntero del mouse y lo siguen por toda la pantalla, la w (Normal) desactiva cualquiera de las otras teclas y deja que las particulas se muevan de forma libre e independiente y la d (repel) hace que todas las particulas eviten en un cierto rango al puntero del mouse y se alejen de el y cada vez que el usuario mueve el mouse las particulas se dispersan por la pantalla.

2. ¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?
R//: si nos referimos en trayectoria creo que si porque el patron de cada una es aleatorio y rebotan por las paredes de la pantalla de forma al azar pero las particulas azules y grandes son mas lentas, las rojas y chiquitas se mueven un poco mas rapido y son muchisimas a diferencia de las azules y las verdes se mueven muy rapido, varian algunas de tamaño y velocidad y son muy pocas.

3. Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.
R//: captura 1 (estado inicial):
<img width="1902" height="988" alt="image" src="https://github.com/user-attachments/assets/d28c8b7c-7a9a-43fb-8576-019c3e0dbb9e" />

captura 2 (Stop):
<img width="1917" height="990" alt="image" src="https://github.com/user-attachments/assets/2f370f5b-153a-4a4c-ace8-956ae64f9fb4" />

captura 3 (Attract): 
<img width="1918" height="976" alt="image" src="https://github.com/user-attachments/assets/4f421a49-6465-4ccb-bba0-5acf33281f9c" />

captura 4 (Repel): 
<img width="1918" height="987" alt="image" src="https://github.com/user-attachments/assets/b7b0c16f-28c2-4fa9-9e72-5a114fa4df8c" />

4. ¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.
R//: a la clase Particle se le da una accion de OnNotify para un evento y luego a esos eventos se les asignan un nombre y un estado, en este caso 'repel' es el nombre del evento y se le da la clase RepelState para que luego al asignar la tecla s en el KeyPressed se le notifica con Notify al OnNotify("Stop") para que ejecute esa accion y en este caso, las particulas se alejen.

# Actividad 9: Investiga el patrón observer #
1. Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?
R//: el observer permite que el sujeto notifique a los observadores cuando pasa un cambio de estado o evento especifico, pero sin determinar especificamente que clase o tipo de objeto es cada observador, el problema que resuelve es no ponerle tanto peso al ofapp, ya que sin el, para cambiar la conducta de una particula el ofapp tendria que mirar cual particula es y de que tipo y asignarle un metodo especifico, pero con el observer solo se emite un mensaje global (sea 'stop', 'repel', 'attract', etc) y la particula decide como reacciona a ese mensaje.

2. Dibuja un diagrama que muestre la relación entre `Subject`, `Observer`, `ofApp` y `Particle` en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.
R//:

        ┌─────────────────┐                     ┌─────────────────┐
        │    Subject      │                     │    Observer     │
        ├─────────────────┤                     ├─────────────────┤
        │ - observers     │                    *│ + onNotify()    │
        │ + addObserver() ├────────────────────►│                 │
        │ + notify()      │                     └────────┬────────┘
        └────────┬────────┘                              ▲
                 ▲                                       │ (hereda)
                 │ (hereda)                              │
        ┌────────┴────────┐                     ┌────────┴────────┐
        │      ofApp      │                     │    Particle     │
        ├─────────────────┤                     ├─────────────────┤
        │ - particles     ├────────────────────►│ + onNotify()    │
        │ + keyPressed()  │                     │ + setState()    │
        └─────────────────┘                     └─────────────────┘


3. Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.
R//:

´´´asm
 [Usuario]       ofApp (Sujeto)                       Particle (Observador)
   │                  │                                       │
   │  keyPressed('a') │                                       │
   ├─────────────────►│                                       │
   │                  │ notify("attract")                     │
   │                  ├──────────────────────────────────────►│
   │                  │                                       │ onNotify("attract")
   │                  │                                       ├───────────────────┐
   │                  │                                       │                   │
   │                  │                                       │ setState(Attract) │
   │                  │                                       │◄──────────────────┘

´´´

4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que `ofApp::update` recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.
R//:

