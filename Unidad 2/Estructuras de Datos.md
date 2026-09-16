# Reto 

## ofApp.h

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
