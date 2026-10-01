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


4. ¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que `ofApp::update` recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.
R//:
- menos complique con el ofapp ya que no necesita saber otros detalles internos de las particulas, nada mas que implementan un observer
- si se quiere agregar otro observador solo se le agrega con addObserver() y no hay que modificar de manera extensa y compleja el codigo
- eliminar las variables globales grandes dentro de update() para determinar quien reacciona con que evento y facilitar el proceso en el codigo.

# Actividad 10: Investiga el Patrón Factory Method #

1. Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?
R//: es un superclase que a partir de las clases que crean, estas clases puede cambiar el tipo de objeto que van a ser o que crearan, y soluciona tener regado por todo el codigo el mismo tipo de nueva clase, facilita tener todo organizado y manejar todo de forma mas sencilla y ordenanda.

2. ¿Qué ventajas aporta el uso de `ParticleFactory` en `ofApp::setup` en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir *nuevos* tipos de partículas en el futuro.
R//: 
- menos carga en el OfApp ya que la creacion y la instancia de las particulas queda en el ParticleFactory y el OfApp solo tiene que parametrizar y coordinar la aplicacion.
- mas orden en el codigo y lo simplifica para no estar espariendo la nueva particula por todo el codigo.
- se puede agregar nuevos tipos de particulas o modificar las ya existenes de forma mas facil y desde el mismo ParticleFactory.

3. Imagina que quieres añadir un nuevo tipo de partícula llamada `"black_hole"` que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la `ParticleFactory` existente. ¿Tendrías que modificar `ofApp::setup`? ¿Por qué sí o por qué no?
R//: paso 1: crear la nueva particula en el ParticleFactory:

        Particle* ParticleFactory::createParticle(const std::string& type) {
        	Particle* particle = new Particle();
        	if (type == "black_hole") {
        		particle->size = ofRandom(80.0f, 90.0f);
        		particle->color = ofColor(500, 500, 500); //porque el fondo es negro toco ponerlo blanco, pero se entiende 
        	}
paso 2: agregar el addObserver en la parte deo fApp::setup():

        void ofApp::setup() {
	ofBackground(0);
	particles.reserve(100 + 5 + 10);
	for (int i = 0; i < 100; ++i) {
		Particle* p = ParticleFactory::createParticle("star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 5; ++i) {
		Particle* p = ParticleFactory::createParticle("shooting_star");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 10; ++i) {
		Particle* p = ParticleFactory::createParticle("planet");
		particles.push_back(p);
		addObserver(p);
	}
	for (int i = 0; i < 1; ++i) {
		Particle* p = ParticleFactory::createParticle("black_hole"); // este es
		particles.push_back(p);
		addObserver(p);
	}

paso 3: ejecutar y disfrutar:

<img width="1709" height="1007" alt="image" src="https://github.com/user-attachments/assets/01f1bb1b-d114-4fb8-95ab-9a5816a7f0bd" />


4. El método `createParticle` en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de `ParticleFactory` y un método de instancia `createParticle()`?.
R//:
- evita estar duplicando la logica de creacion en varias partes de la app, si cambia la forma de construir de una particula cambia solo se cambia el ParticleFactory y ya
- evita y esconde detalles e instrucciones complejas en el codigo que permite tener una interfaz mas limpia
- mete una clase mas al proyecto, que en casos puede ser innecesaria si la creacion de objetos es simple

# Actividad 11: Investiga el patrón State #

1. Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?
R//: es literalmente una alterrnativa al estar llenando de IF el codigo para que cada cosa cambie de estado, esto sirve como alternativa para simplificar esos procesos de estado y permite asignarle a los objetos ejecuciones independientes para esos cambios de estado sin tener todos eso bloques gigantes en la clase principal. Es bueno aplicarlo cuando hay varios objetos y cuando se quiere agregar varios estados como en el caso de estudio que hay varias particulas y varios cambios de estado, esto sirve para simplificar el codigo y no tener un despelote de cosas en el codigo.

2. Dibuja un diagrama de estados simple para la clase `Particle`. Muestra los diferentes estados (`Normal`, `Attract`, `Repel`, `Stop`) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘w’, ‘a’, ‘d’, ‘s’).
R//: 

                             ┌──────────────┐
                             │ NormalState  │◄──────────────────┐
                             └──────┬───────┘                   │
                                    │                           │
                  ┌─────────────────┼─────────────────┐         │
                  │ 'a'             │ 'd'             │ 's'     │ 'w'
                  ▼                 ▼                 ▼         │
          ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
          │ AttractState │  │  RepelState  │  │  StopState   │  │
          └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  │
                 │                 │                 │          │
                 └─────────────────┴─────────────────┴──────────┘


3. Describe las ventajas de usar el patrón State en `Particle` en lugar de tener un miembro `std::string estadoActual` y usar un gran `if/else if/else` o `switch` dentro de `Particle::update()` para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).
R//: 
- cada comportamiento dentro del state se queda en su propia clase sin necesidad de entender como funciona lo de atraer o para o explulsar, solo le da la ejecucion a state->onEnter(this);.
- para añadir un nuevo estado no hay necesidad de editar completo el Particle::update() solo se le agrega una clase heredera de state con el estado que se le quiere dar (por ejemplo StopState) y ya.
- mejora al limpiar en el cambio de estado sin agregar condicionales adicionales.

4. ¿Qué responsabilidad tienen los métodos `onEnter` y `onExit` en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en *todos* los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en `onEnter` para `AttractState` o en `onExit` para `StopState`?
R//: onEnter y onExit vuelven de forma automatica la limpieza cuando se ejecuta Particle::setState() dejando que la configuracion para entrar y salir de ese estado este en la clase donde esta el estado. por ejemplo el onEnter en AttractState podria usarse por si quiero agregar que cambie de velocidad de forma aleatoria en un rango sin tener que editar medio codigo y dar mil explicaciones:

        void AttractState::onEnter(Particle* particle) {
        	particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));

# Sesión 7: Aplicación #
## Actividad 12 ##

1. El código fuente completo de tu proyecto openFrameworks.
R//:

OfApp.h:

        #pragma once
        #include "ofMain.h"
        #include <string>
        #include <vector>
        class Observer {
        public:
        	virtual ~Observer() = default;
        	virtual void onNotify(const std::string& event) = 0;
        };
        class Subject {
        public:
        	void addObserver(Observer* observer);
        	void removeObserver(Observer* observer);
        protected:
        	void notify(const std::string& event);
        private:
        	std::vector<Observer*> observers;
        };
        
        class Particle;
        
        class State {
        public:
        	virtual ~State() = default;
        	virtual void update(Particle* particle) = 0;
        	virtual void onEnter(Particle* particle) {}
        	virtual void onExit(Particle* particle) {}
        };
        
        class Particle : public Observer {
        public:
        	Particle();
        	~Particle() override;
        	Particle(const Particle&) = delete;
        	Particle& operator=(const Particle&) = delete;
        	void update();
        	void draw();
        	void onNotify(const std::string& event) override;
        	void setState(State* newState);
        	ofVec2f position;
        	ofVec2f velocity;
        	float size;
        	ofColor color;
        private:
        	void keepInsideWindow();
        	State* state;
        };
        
        class NormalState : public State {
        public:
        	void update(Particle* particle) override;
        	void onEnter(Particle* particle) override;
        };
        
        class AttractState : public State {
        public:
        	void update(Particle* particle) override;
        };
        
        class RepelState : public State {
        public:
        	void update(Particle* particle) override;
        };
        
        class StopState : public State {
        public:
        	void update(Particle* particle) override;
        };
        
        class Shakestate : public State {
        public:
        	void update(Particle* particle) override;
        };
        
        class ParticleFactory {
        public:
        	static Particle* createParticle(const std::string& type);
        };
        
        class ofApp : public ofBaseApp, public Subject {
        public:
        	~ofApp() override;
        	void setup() override;
        	void update() override;
        	void draw() override;
        	void keyPressed(int key) override;
        private:
        	std::vector<Particle*> particles;
        };


OfApp.cpp

        #include "ofApp.h"
        #include <algorithm>
        void Subject::addObserver(Observer* observer) {
        	if (!observer) return;
        	if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
        		observers.push_back(observer);
        	}
        }
        
        void Subject::removeObserver(Observer* observer) {
        	if (!observer) return;
        	observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
        }
        void Subject::notify(const std::string& event) {
        	for (Observer* observer : observers) {
        		observer->onNotify(event);
        	}
        }
        Particle::Particle() : state(nullptr) {
        	position = ofVec2f(ofRandomWidth(), ofRandomHeight());
        	velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
        	size = ofRandom(2.0f, 5.0f);
        	color = ofColor(255);
        	state = new NormalState();
        	state->onEnter(this);
        }
        
        Particle::~Particle() {
        	if (state) {
        		state->onExit(this);
        		delete state;
        		state = nullptr;
        	}
        }
        void Particle::setState(State* newState) {
        	if (state) {
        		state->onExit(this);
        		delete state;
        	}
        	state = newState;
        	if (state) {
        		state->onEnter(this);
        	}
        }
        void Particle::update() {
        	if (state) {
        		state->update(this);
        	}
        	keepInsideWindow();
        }
        void Particle::draw() {
        	ofPushStyle();
        	ofSetColor(color);
        	ofDrawCircle(position, size);
        	ofPopStyle();
        }
        void Particle::onNotify(const std::string& event) {
        	if (event == "attract") {
        		setState(new AttractState()); 
        	}
        	else if (event == "repel") {
        		setState(new RepelState());
        	}
        	else if (event == "stop") {
        		setState(new StopState());
        	}
        	else if (event == "normal") {
        		setState(new NormalState());
        	}
        	else if (event == "shake") {
        		setState(new Shakestate());
        
        	}
        }
        
        void Particle::keepInsideWindow() {
        	const float W = static_cast<float>(ofGetWidth());
        	const float H = static_cast<float>(ofGetHeight());
        	if (position.x < 0.0f) {
        		position.x = 0.0f;
        		velocity.x *= -1.0f;
        	}
        	else if (position.x > W) {
        		position.x = W;
        		velocity.x *= -1.0f;
        	}
        	if (position.y < 0.0f) {
        		position.y = 0.0f;
        		velocity.y *= -1.0f;
        	}
        	else if (position.y > H) {
        		position.y = H;
        		velocity.y *= -1.0f;
        	}
        }
        
        
        void NormalState::onEnter(Particle* particle) {
        	particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
        }
        void NormalState::update(Particle* particle) {
        	particle->position += particle->velocity;
        }
        static void steer(Particle* particle, const ofVec2f& toward, float accel, float vmax, float posScale) {
        	ofVec2f dir = toward - particle->position;
        	float len = dir.length();
        	if (len > 1e-6f) {
        		dir /= len;
        		particle->velocity += dir * accel;
        	}
        	particle->velocity.limit(vmax);
        	particle->position += particle->velocity * posScale;
        }
        
        void AttractState::update(Particle* particle) {
        	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
        	steer(particle, mouse, 0.05f, 3.0f, 0.2f);
        }
        void RepelState::update(Particle* particle) {
        	ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
        	ofVec2f away = particle->position - mouse;
        	float len = away.length();
        	if (len > 1e-6f) {
        		away /= len;
        		particle->velocity += away * 0.05f;
        	}
        	particle->velocity.limit(3.0f);
        	particle->position += particle->velocity * 0.2f;
        }
        void StopState::update(Particle* particle) {
        	particle->velocity *= 0.80f;
        	if (particle->velocity.lengthSquared() < 1e-4f) {
        		particle->velocity.set(0.0f, 0.0f);
        	}
        	particle->position += particle->velocity;
        }
        void Shakestate::update(Particle* particle) {
        	particle->velocity.set(ofRandom(-1.0f, 1.0f), ofRandom(-1.0f, 1.0f));
        	particle->position += particle->velocity;
        }
        Particle* ParticleFactory::createParticle(const std::string& type) {
        	Particle* particle = new Particle();
        	if (type == "star") {
        		particle->size = ofRandom(2.0f, 4.0f);
        		particle->color = ofColor(255, 0, 0);
        	}
        	else if (type == "shooting_star") {
        		particle->size = ofRandom(3.0f, 6.0f);
        		particle->color = ofColor(0, 255, 0);
        		particle->velocity *= 3.0f;
        	}
        	else if (type == "planet") {
        		particle->size = ofRandom(5.0f, 8.0f);
        		particle->color = ofColor(0, 0, 255);
        	}
        	else if (type == "neutron_star") {
        		particle->size = ofRandom(80.0f, 90.0f);
        		particle->color = ofColor(500, 500, 500);
        	}
        	return particle;
        }
        ofApp::~ofApp() {
        	for (Particle* p : particles) {
        		removeObserver(p);
        		delete p;
        	}
        	particles.clear();
        }
        void ofApp::setup() {
        	ofBackground(0);
        	particles.reserve(100 + 5 + 10);
        	for (int i = 0; i < 100; ++i) {
        		Particle* p = ParticleFactory::createParticle("star");
        		particles.push_back(p);
        		addObserver(p);
        	}
        	for (int i = 0; i < 5; ++i) {
        		Particle* p = ParticleFactory::createParticle("shooting_star");
        		particles.push_back(p);
        		addObserver(p);
        	}
        	for (int i = 0; i < 10; ++i) {
        		Particle* p = ParticleFactory::createParticle("planet");
        		particles.push_back(p);
        		addObserver(p);
        	}
        	for (int i = 0; i < 1; ++i) {
        		Particle* p = ParticleFactory::createParticle("neutron_star");
        		particles.push_back(p);
        		addObserver(p);
        	}
        }
        void ofApp::update() {
        	for (Particle* p : particles) {
        		p->update();
        	}
        }
        void ofApp::draw() {
        	for (Particle* p : particles) {
        		p->draw();
        	}
        }
        void ofApp::keyPressed(int key) {
        	switch (key) {
        	case 's':
        		notify("stop");
        		break;
        	case 'a':
        		notify("attract");
        		break;
        	case 'd':
        		notify("repel");
        		break;
        	case 'w':
        		notify("normal");
        		break;
        	default:
        		break;
        	case 'q':
        		notify("shake");
        		break;
        	}
        }


3. Explica cómo usaste el patrón Factory para esta nueva partícula.
R//: me copie del ejemplo de uno de los ejercicos del agujero negro y cree una estrella de neutrones gigante que va a todos lados, la añadi desde el ofApp::setup() y la agregue tambien a Particle* ParticleFactory::createParticle para poder determinar su velocidad y color (estuve 20 minutos decidiendo que color).

4. Describe cómo implementaste el patrón Observer para esta nueva partícula.
R//: lo agregue en el  ofApp::setup() creando una nueva para la estrella de neutrones le di addObserver(p); para que el cambio de estado lo detecte y ejecute dicho estado (le puse otro estado mas q: shake)

5. Explica cómo aplicaste el patrón State a esta nueva partícula.
R//: cree una nueva clase llamada Shakestate que hace que las particulas se detengan y tiemblen, lo defini en el .h para luego poder agregarlo en Particle::onNotify y le configure la velocidad y la posicion donde se sacuden para que la particula se detenga y tiemble pero en su sitio, pero esto fue solo porque quise al tener el addObserver(p); de por si la estrella de neutrones ya tiene para ejecutar los estados y los cambios de estado con  todas las particulas.
