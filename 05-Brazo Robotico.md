---
layout: default
title: Brazo robotico
nav_order: 5
---

## Brazo robótico

Este proyecto consistió en construir un brazo robótico de MDF con cuatro servomotores, controlado con un Arduino UNO. Cada articulación se mueve con su propio potenciómetro, así que al girarlo el servo correspondiente se coloca en el ángulo que se indica.

### Materiales

Arduino UNO y cable USB, protoboard, jumpers, cuatro potenciómetros, cuatro servomotores y piezas de MDF cortadas con laser para la estructura. Tres de los servomotores son MG995, que son más grandes y tienen más fuerza, y el cuarto es un servo azul pequeño, igual al que se usó en las prácticas anteriores.

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 1.png){: width="200"}


### Conexiones

Cada potenciómetro se conecta a una entrada analógica del Arduino y cada servomotor a una salida digital con PWM: A0, A1, A2, A3. Los servomotores comparten tierra con el Arduino.

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 2.png){: width="200"}


![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 3.png){: width="200"}


![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 4.png){: width="200"}


### Alimentación

Los servomotores MG995 consumen bastante más corriente que uno pequeño, sobre todo cuando mueven carga. Por eso conviene alimentarlos con una fuente externa de 5 V y no desde el pin de 5 V del Arduino, que no aguanta tanto. Lo importante es unir la tierra de la fuente con la tierra del Arduino.

### Código

El programa lee cada potenciómetro, convierte el valor de 0 a 1023 en un ángulo de 0 a 170 grados con map y se lo envía al servomotor correspondiente.

```cpp
#include <Servo.h>

Servo servoBase;
Servo servoHombro;
Servo servoCodo;
Servo servoPinza;

// Potenciómetros
const int potBase   = A0;
const int potHombro = A1;
const int potCodo   = A2;
const int potPinza  = A3;

// Pines de señal de los servos
const int pinBase   = 3;
const int pinHombro = 5;
const int pinCodo   = 6;
const int pinPinza  = 9;

void setup() {

  servoBase.attach(pinBase);
  servoHombro.attach(pinHombro);
  servoCodo.attach(pinCodo);
  servoPinza.attach(pinPinza);

}

void loop() {

  // Leer potenciómetros
  int lecturaBase   = analogRead(potBase);
  int lecturaHombro = analogRead(potHombro);
  int lecturaCodo   = analogRead(potCodo);
  int lecturaPinza  = analogRead(potPinza);

 // Convertir lectura 0-1023 a grados

  int anguloBase =
    map(lecturaBase, 0, 1023, 0, 170);

  int anguloHombro =
    map(lecturaHombro, 0, 1023, 0, 170);

  int anguloCodo =
    map(lecturaCodo, 0, 1023, 0, 170);

  int anguloPinza =
    map(lecturaPinza, 0, 1023, 0, 170);
  

  // Mover servos

  servoBase.write(anguloBase);
  servoHombro.write(anguloHombro);
  servoCodo.write(anguloCodo);
  servoPinza.write(anguloPinza);
  
  delay(15);
}
```

### Construcción -

Primero se cortaron las piezas de MDF con una cortadora laser y se ensambló la base y los segmentos del brazo. Después se fijó cada servomotor en su articulación y se conectaron los potenciómetros. Donde unos de los problemas fue el peso de los servos pero se pudo solucionar rapaido.

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 1.png){: width="200"}

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 7.png){: width="200"}

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 4.png){: width="200"}

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 2.png){: width="200"}

![Figura 3 — GitHub](/assets/brazo/videos/fotos/brazo 6.png){: width="200"}

### Resultado -

El brazo responde al movimiento de cada potenciómetro de forma independiente. Al usar servomotores MG995 en las articulaciones principales, el movimiento tiene más fuerza que con los servos pequeños. Aunque el brazo tiende a vibrar un poco ya que la energia que consume es demasiada y no esta del todo fijo.

A pesar de todo el brazo cumplio con aguantar la pelota segundos y de pasarla pelota a otro braso robotico.

<video muted controls width="600">
  <source src="{{ '/assets/brazo/videos/fotos/WhatsApp Video 2026-10-01 at 16.41.45.mp4' | relative_url }}" type="video/mp4">
</video>

<video muted controls width="600">
  <source src="{{ '/assets/brazo/videos/fotos/WhatsApp Video 2026-10-01 at 16.41.45.mp4' | relative_url }}" type="video/mp4">
</video>

### Conclusión -

Con este proyecto se aplicó lo visto en las prácticas de servomotores y potenciómetros en un sistema completo. También se vio que elegir bien los servomotores y su alimentación es importante para que el brazo funcione de forma estable. 