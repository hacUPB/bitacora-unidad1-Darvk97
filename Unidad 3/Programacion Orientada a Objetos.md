# Actividad 1 – Diagnóstico inicial
## Parte 1. Recordando los conceptos (C#)

1. ¿Qué es el encapsulamiento?

R//: Para mí, el encapsulamiento es proteger los datos de un objeto para que no puedan modificarse directamente desde cualquier parte del programa. En lugar de acceder a las variables, se usan propiedades o métodos públicos para controlar cómo cambian esos datos. Esto hace que el código sea más seguro y organizado

Ejemplo: En un juego hecho en Unity, la vida del jugador era privada y solo podía cambiar mediante un método como RecibirDaño(). Así evitaba que otra clase pusiera la vida en un valor inválido.

2. ¿Qué es la herencia?

R//: La herencia permite crear una clase nueva a partir de otra ya existente. La clase hija hereda los atributos y métodos de la clase padre y además puede agregar nuevas características o modificar su comportamiento. Se usa para reutilizar código y evitar escribir lo mismo varias veces. 

Ejemplo:
Clase padre: Vehiculo
Clase hija: Moto
La moto hereda velocidad, marca y arrancar, pero además tiene el atributo cilindraje.

3. ¿Qué es el polimorfismo?

R//: El polimorfismo significa que un mismo método puede comportarse de forma diferente según el tipo real del objeto. Es decir, diferentes clases responden al mismo mensaje con su propia implementación.

## Parte 2. Análisis del código (C#)

### Encapsulamiento:

private string nombre;

Es un ejemplo claro porque la variable está protegida y no puede modificarse directamente desde otra clase, solo se accede mediante la propiedad Nombre.

¿Por qué nombre es private y Nombre es public?

R//: Porque el dato se protege y la propiedad controla el acceso. Así se evita que cualquier clase cambie el nombre de la figura de manera incorrecta o accidental. Es una forma de ocultar la implementación interna del objeto.

### Herencia

¿Cómo se evidencia la herencia en Circulo?

Se observa en esta línea:

public class Circulo : Figura

indica que Circulo hereda de Figura, por lo que obtiene todos sus métodos y atributos públicos o protegidos.

¿Qué otros datos almacena además de Radio?

R//: Gracias a la herencia también almacena:

- Nombre

- El campo privado nombre (administrado por la clase padre)

Es decir, un objeto Circulo contiene tanto los datos propios como los heredados.

### Polimorfismo

¿Cómo funciona fig.Dibujar()?

R//: cada objeto guarda una referencia al tipo real que es. Cuando el programa ejecuta fig.Dibujar(), primero mira si el objeto es un Circulo o un Rectangulo y luego llama automáticamente al método correspondiente. El compilador sabe que existe el método porque pertenece a Figura, pero la decisión final ocurre cuando el programa está ejecutándose.

## Parte 3. Hipótesis sobre la implementación

1. Memoria y herencia

R//: El objeto se guarda como un único bloque de memoria, primero aparecen los datos heredados de Figura y luego los propios de Rectangulo. La herencia no crea dos objetos separados; forma un único objeto con datos heredados y propios.

2. El mecanismo del polimorfismo

R//: Cada objeto tiene una especie de tabla donde están guardadas las funciones que le corresponden. Cuando se llama fig.Dibujar(), el programa consulta esa tabla y ejecuta la versión correcta del método según el tipo del objeto. Más adelante descubriré que esa tabla es la vtable.

3. La barrera del encapsulamiento

R//: El compilador revisa los modificadores private, protected y public antes de generar el programa. Si intento acceder a un miembro privado desde otra clase, aparece un error de compilación y el programa ni siquiera se ejecuta. Por eso creo que el encapsulamiento se garantiza principalmente en tiempo de compilación, no como una barrera absoluta en la memoria.

# Actividad 2. Aplicacion

R//: La aplicación simula un espectáculo de fuegos artificiales utilizando programación orientada a objetos. Cada vez que el usuario hace clic, se crea una RisingParticle que asciende desde la parte inferior de la pantalla y, al llegar a cierta altura o terminar su tiempo de vida, explota generando nuevas partículas de diferentes tipos (CircularExplosion, RandomExplosion o StarExplosion). Todas las partículas se almacenan en un mismo vector y se actualizan y dibujan mediante polimorfismo, mientras que las que terminan su ciclo de vida son eliminadas para liberar la memoria.

# Actividad 3.

Hipótesis
R//: Esperaba encontrar un objeto ofApp que almacenara principalmente el vector particles y los datos heredados de ofBaseApp.

Captura: Objeto ofApp en Autos/Locals.

Observación
R//: El depurador muestra que ofApp contiene un std::vector<Particle*>, donde cada elemento es un puntero a un objeto diferente. También aparecen los datos heredados de la clase base.

Captura: Objeto CircularExplosion en Memory 1.

Observación
R//: El objeto aparece como un único bloque de memoria. Dentro de él primero aparece la parte correspondiente a Particle, luego ExplosionParticle y finalmente los datos propios de CircularExplosion.

Conclusiónes
R//: La herencia no crea varios objetos separados; todos los datos se almacenan dentro del mismo objeto siguiendo la jerarquía de clases.
La vtable

Captura: _vtable de CircularExplosion.

Observación

La tabla contiene direcciones de funciones como:

- update

- draw

- isDead

- Destructor

Captura: _vtable de StarExplosion.

Comparación

R//: Las tablas tienen prácticamente la misma estructura, pero la dirección del método draw() es diferente porque cada clase implementa su propia versión.

Conclusión

R//: La vtable es una tabla de punteros a funciones virtuales. Gracias a ella el programa puede decidir qué método ejecutar en tiempo de ejecución.

# Actividad 4

```asm
class AccessControl {
private:
		int privateVar;
protected:
		int protectedVar;
public:
		int publicVar;
		AccessControl() : privateVar(1), protectedVar(2), publicVar(3) {}
		};
int main() {
		AccessControl ac;
		ac.publicVar = 10;
		// Válido
		// ac.protectedVar = 20;
		// Error de compilación
		// ac.privateVar = 30;
		// Error de compilación
		return 0;
		}
```

Al descomentar:

```asm
ac.protectedVar = 20;
ac.privateVar = 30;
```

el programa no compila.

¿Por qué?
R//: Porque protected solo puede accederse desde clases hijas y private únicamente desde la propia clase.

Conclusión
R//: El encapsulamiento es una protección aplicada por el compilador antes de ejecutar el programa.

```asm
#include <iostream>
class MyClass {
private:
		int secret1;
		float secret2;
		char secret3;
public:
		MyClass(int s1, float s2, char s3) : secret1(s1), secret2(s2), secret3(s3) {}
    void printMembers() const {
		    std::cout << "secret1: " << secret1 << "\n";
		    std::cout << "secret2: " << secret2 << "\n";
		    std::cout << "secret3: " << secret3 << "\n";
		    }
		};

int main() {
		MyClass obj(42, 3.14f, 'A');
		// Esta línea causará un error de compilación
		std::cout << obj.secret1 << std::endl;
    obj.printMembers();
    // Método público para mostrar los valores
    return 0;
    }
```

el programa imprime:

```asm
secret1: 42
secret2: 3.14
secret3: A
```
Compila el programa y ejecuta. 

```asm
#include <iostream>
class MyClass {
private:
		int secret1;
		float secret2;
		char secret3;
public:
		MyClass(int s1, float s2, char s3) : secret1(s1), secret2(s2), secret3(s3) {}
    void printMembers() const {
		    std::cout << "secret1: " << secret1 << "\n";
		    std::cout << "secret2: " << secret2 << "\n";
		    std::cout << "secret3: " << secret3 << "\n";
		    }
		};
int main() {
		MyClass obj(42, 3.14f, 'A');
    // Usando reinterpret_cast para violar el encapsulamiento
    int* ptrInt = reinterpret_cast<int*>(&obj);
    float* ptrFloat = reinterpret_cast<float*>(ptrInt + 1);
    char* ptrChar = reinterpret_cast<char*>(ptrFloat + 1);
    // Accediendo y mostrando los valores privados
    std::cout << "Accediendo directamente a los miembros privados:\n";
    std::cout << "secret1: " << *ptrInt << "\n";
    // Accede a secret1
    std::cout << "secret2: " << *ptrFloat << "\n";
    // Accede a secret2
    std::cout << "secret3: " << *ptrChar << "\n";
    // Accede a secret3
    return 0;
    }
```

Conclusión
R//:Aunque el compilador impide acceder a miembros privados, en memoria esos datos siguen existiendo. Por eso el encapsulamiento es una protección de acceso al código, no un cifrado de la memoria.

¿Qué es el encapsulamiento?
R//: Es el principio que protege el estado interno de los objetos mediante modificadores de acceso (private, protected y public). Es importante porque evita modificaciones indebidas y hace el código más seguro y mantenible.

# Actividad 5

captura de nuevo la memoria que ocupa el objeto CircularExplosion compara la jerarquía de clases con los campos en memoria del objeto. ¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?
R//:

1. Captura: 

2. Los campos aparecen en este orden:
- _vtable
- position
- velocity
- color
- age
- lifetime
- size

3. conclusion: Cada clase agrega sus propios atributos al final del bloque heredado.

¿Cómo se implementa la herencia en C++?
R//: C++ coloca primero los datos de la clase base y luego los de la clase hija dentro del mismo objeto. Así un puntero a Particle puede apuntar correctamente a un CircularExplosion.

C++ permite hacer algo que C# no: herencia múltiple. Realiza un experimento que te permita ver cómo se objeto en memoria cuya clase base tiene herencia múltiple.
R//: 

```asm
class A{
public:int a;
};

class B{
public:int b;
};

class C : public A, public B{
public:int c;
};
```

La herencia múltiple incorpora primero la memoria de cada clase base y luego los datos de la clase derivada.

# Actividad 6

<img width="720" height="489" alt="image" src="https://github.com/user-attachments/assets/1ab0d493-aad7-4082-862d-b561e0433b28" />

¿Qué relación existe entre métodos virtuales y polimorfismo?
R//: Los métodos virtuales hacen posible el polimorfismo. La vtable guarda las direcciones de las funciones y, cuando un puntero de tipo Particle llama update(), el programa consulta esa tabla para ejecutar la implementación correcta del objeto real.

# Actividad 7

1. Agrega dos nuevos tipos de Particle diferentes a RisingParticle.
R//:

createRisingParticle() (ofApp.cpp)

```asm
void ofApp::createRisingParticle() {

    float minX = ofGetWidth() * 0.35;
    float maxX = ofGetWidth() * 0.65;
    float spawnX = ofRandom(minX, maxX);

    glm::vec2 pos(spawnX, ofGetHeight());

    glm::vec2 target(
        ofGetWidth()/2 + ofRandom(-300,300),
        ofGetHeight()*0.10 + ofRandom(-30,30));

    glm::vec2 direction = glm::normalize(target - pos);
    glm::vec2 vel = direction * ofRandom(250,350);

    ofColor col;
    col.setHsb(ofRandom(255),220,255);

    float lifetime = ofRandom(1.5,3.5);

    int type = (int)ofRandom(3);

    if(type == 0)
        particles.push_back(new RisingParticle(pos, vel, col, lifetime));
    else if(type == 1)
        particles.push_back(new ZigZagParticle(pos, vel, col, lifetime));
    else
        particles.push_back(new SpiralParticle(pos, vel, col, lifetime));
}
```

update() (ofApp.cpp)

```asm
void ofApp::update() {

    float dt = ofGetLastFrameTime();

    for(int i=0;i<particles.size();i++)
        particles[i]->update(dt);

    for(int i=particles.size()-1;i>=0;i--){

        if(particles[i]->shouldExplode()){

            int explosionType = (int)ofRandom(4);
            int numParticles = (int)ofRandom(20,30);

            for(int j=0;j<numParticles;j++){

                if(explosionType==0)
                    particles.push_back(new CircularExplosion(
                        particles[i]->getPosition(),
                        particles[i]->getColor()));

                else if(explosionType==1)
                    particles.push_back(new RandomExplosion(
                        particles[i]->getPosition(),
                        particles[i]->getColor()));

                else if(explosionType==2)
                    particles.push_back(new StarExplosion(
                        particles[i]->getPosition(),
                        particles[i]->getColor()));

                else
                    particles.push_back(new FireworkExplosion(
                        particles[i]->getPosition(),
                        particles[i]->getColor()));
            }

            delete particles[i];
            particles.erase(particles.begin()+i);
        }
        else if(particles[i]->isDead()){
            delete particles[i];
            particles.erase(particles.begin()+i);
        }
    }
}
```

ZigZagParticle (ofApp.h):

```asm
class ZigZagParticle : public RisingParticle {
public:
    ZigZagParticle(const glm::vec2& pos,
        const glm::vec2& vel,
        const ofColor& col,
        float life)
        : RisingParticle(pos, vel, col, life) {
    }

    void update(float dt) override {
        RisingParticle::update(dt);
        position.x += sin(age * 10.0f) * 120.0f * dt;
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, 8);
    }
};
```

SpiralParticle (ofApp.h):

```asm
class SpiralParticle : public RisingParticle {
public:
    SpiralParticle(const glm::vec2& pos,
        const glm::vec2& vel,
        const ofColor& col,
        float life)
        : RisingParticle(pos, vel, col, life) {
    }

    void update(float dt) override {
        RisingParticle::update(dt);
        position.x += cos(age * 12.0f) * 80.0f * dt;
        position.y += sin(age * 12.0f) * 30.0f * dt;
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, 8);
    }
};
```

2. Implementar un nuevo modo de explosión.
R//:

FireworkExplosion (ofApp.h)

```asm
class FireworkExplosion : public ExplosionParticle {
public:
    FireworkExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 2.0f, ofRandom(4, 8)) {

        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(140, 260);

        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }

    void update(float dt) override {
        position += velocity * dt;

        velocity *= 0.99f;
        velocity.y += 140 * dt;

        age += dt;

        float alpha = ofMap(age, 0, lifetime, 255, 0, true);
        color.a = alpha;
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, size);
    }
};
```
