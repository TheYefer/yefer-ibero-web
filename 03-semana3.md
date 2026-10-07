---
layout: default
title: Semana 3 Práctica Arduino
nav_order: 4
---

## Semana 3

Durante esta semana se realizaron prácticas con Arduino UNO para conocer sus entradas y salidas digitales y analógicas. Se trabajó con LEDs, un display de 7 segmentos, botones, servomotores y potenciómetros.

## Materiales

- Arduino UNO y cable USB
- Protoboard y jumpers
- LEDs y resistencias
- Display de 7 segmentos
- Botones
- Potenciómetros
- Servomotores

---

### Práctica 01 - Parpadeo del LED integrado

Se programó el LED que ya trae la placa Arduino (pin 13) para que se encienda y se apague en intervalos de un segundo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 01-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 01
```

### Práctica 03 - Uso de delay

Se probó la función `delay` para controlar cuánto tiempo permanece el LED encendido y apagado, usando pausas de un segundo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 03-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 03
```

### Práctica 04 - LED conectado directamente al Arduino

Se conectó un LED externo directo a la placa y se repitió el parpadeo con el mismo programa.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 04-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 04
```

### Práctica 05 - Circuito con resistencia para el LED

Se armó el circuito en la protoboard agregando una resistencia que protege al LED, y se mantuvo el parpadeo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 05-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 05
```

### Práctica 06 - Dos LEDs alternando

Se añadió un segundo LED con su resistencia. El programa los enciende uno después del otro.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 06-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 06
```

### Práctica 07 - Dos LEDs al mismo tiempo

Con el mismo circuito de dos LEDs, el programa los enciende y los apaga a la vez.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 07-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 07
```

### Práctica 08 - Display de 7 segmentos

Se conectó un display de 7 segmentos y se enviaron señales HIGH y LOW a cada segmento para mostrar un número.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 08-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 08
```

### Práctica 10 - Entrada digital con botón

Se usó un botón como entrada digital: el LED se enciende mientras el botón está presionado.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 10-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 10
```

### Práctica 12 - Entrada digital con condición

Se leyó el botón dentro de una condición `if` / `else`: si está presionado se enciende el LED y si no, se apaga.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 12-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 12
```

### Práctica 13 - Condición con dos botones

Mismo principio de la práctica anterior, pero con dos botones y dos LEDs, cada botón controlando su LED.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 13-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 13
```

### Práctica 14 - Condición OR

Se simuló una compuerta OR: el LED se enciende si se presiona uno de los botones o los dos.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 14-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 14
```

### Práctica 15 - Condición AND

Se simuló una compuerta AND: el LED solo se enciende cuando se presionan los dos botones al mismo tiempo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 15-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 15
```

### Práctica 16 - Contador con LEDs

Cada vez que se presiona el botón se enciende un LED más. Al llegar al máximo, la cuenta se reinicia.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 16-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 16
```

### Práctica 17 - Inicio del servomotor

Se conectó un servomotor y se programó para que se coloque en una posición fija.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 17-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 17
```

### Práctica 18 - Posiciones del servomotor

El servomotor recorre una secuencia de posiciones (0, 90 y 180 grados) con una pausa entre cada una.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 18-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 18
```

### Práctica 19 - Un servomotor con potenciómetro

La posición del servomotor se controla girando un potenciómetro. El código convierte la lectura analógica en un ángulo de 0 a 180 grados.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 19-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 19
```

### Práctica 19 - Parte 2 - Dos servomotores con un potenciómetro

Se agregó un segundo servomotor y ambos se mueven con un solo potenciómetro.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 19_2-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 19 - Parte 2
```

### Práctica 20 - Dos servomotores con dos potenciómetros

Cada servomotor tiene su propio potenciómetro, así que se mueven de forma independiente.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 20-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 20
```

### Práctica 20 - Parte 2 - Dos servomotores con dos potenciómetros (segunda toma)

Segunda grabación del mismo circuito, mostrando con más detalle el movimiento independiente de cada servo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 20_2-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 20 - Parte 2
```

### Práctica 21 - Servomotor con fuente externa

El servomotor se alimenta con una fuente externa en lugar del Arduino, para darle la potencia que necesita.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 21-converted.mp4' | relative_url }}" type="video/mp4">
</video>

Código:

```cpp
// Pega aquí tu código de la práctica 21
```

---

## Conclusión

[Escribe aquí qué aprendiste, qué te costó más trabajo y cómo podrías usar esto en un proyecto.]
