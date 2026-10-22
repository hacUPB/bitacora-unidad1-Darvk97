# Reto 

## ofApp.h

```asm
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius),
          color(_color), opacity(_opacity), next(nullptr) {}
};

// Cola FIFO
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};

// Constructor
BrushQueue::BrushQueue(int _maxSize) {
    front = nullptr;
    rear = nullptr;
    size = 0;
    maxSize = _maxSize;
}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Agregar al final
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {

    Node* nuevo = new Node(x, y, radius, color, opacity);

    if (isEmpty()) {
        front = nuevo;
        rear = nuevo;
    }
    else {
        rear->next = nuevo;
        rear = nuevo;
    }

    size++;

    if (size > maxSize) {
        dequeue();
    }
}

// Eliminar el más antiguo
void BrushQueue::dequeue() {

    if (isEmpty()) return;

    Node* temp = front;
    front = front->next;

    delete temp;
    size--;

    if (front == nullptr) {
        rear = nullptr;
    }
}

// Borrar toda la cola
void BrushQueue::clear() {

    while (!isEmpty()) {
        dequeue();
    }
}

// ¿Está vacía?
bool BrushQueue::isEmpty() {
    return front == nullptr;
}


// Aplicación
class ofApp : public ofBaseApp {

public:

    BrushQueue strokes;
    float backgroundHue = 0;

    ofApp() : strokes(50) {}

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};
```

## ofApp.cpp 

```asm
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {

    ofSetFrameRate(60);
    ofEnableAlphaBlending();
}

//--------------------------------------------------------------
void ofApp::update() {

    backgroundHue += 0.2;

    if (backgroundHue > 255)
        backgroundHue = 0;

    // Pintar mientras se mantiene el click 
    if (ofGetMousePressed()) {

        float r = ofRandom(8, 22);

        ofColor c;
        c.setHsb(ofRandom(255), 220, 255);

        strokes.enqueue(ofGetMouseX(),
                        ofGetMouseY(),
                        r,
                        c,
                        255);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {

    // Fondo
    ofColor c1, c2;

    c1.setHsb(backgroundHue, 150, 240);
    c2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);

    ofBackgroundGradient(c1, c2, OF_GRADIENT_LINEAR);

    // Dibujar los trazos
    Node* actual = strokes.front;

    while (actual != nullptr) {

        // Los más antiguos son más claritos
        float alpha = ofMap(actual->opacity, 0, 255, 40, 255);

        ofSetColor(actual->color, alpha);
        ofDrawCircle(actual->x, actual->y, actual->radius);

        actual = actual->next;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {

    // Limpiar pantalla
    if (key == 'c') {
        strokes.clear();
    }

    // Alternar 50 y 100
    if (key == 'a') {

        if (strokes.maxSize == 50)
            strokes.maxSize = 100;
        else
            strokes.maxSize = 50;
    }

    // Guardar captura
    else if (key == 's') {
        ofSaveScreen("captura_" + ofGetTimestampString() + ".png");
    }
}
```
link youtube: https://youtu.be/SRCAQrSGt2k
