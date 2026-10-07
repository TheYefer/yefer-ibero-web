---
layout: default
title: Semana 3 Practica Arduino
nav_order: 4
---

### Reporte 1
Se realizaron diversos códigos en Arduino UNO, así, probando las funciones básicas que posee el microcontrolador por medio de circuitos simples que fueron dados por el profesor, utilizando principalmente entradas y salidas.

Arduino, ¿Qué es?
Arduino es software de código abierto con lnguaje C++, es un software de libre uso y además, tiene diferentes modelos de hard. Fue creado en italia en 2005 para desarrollar prototipos interactivos. Permite el uso de varios modelos de microordenadores a libertad del usuario.

En la mayoría de ellos, su hardware consta de una placa que contiene un microcontrolador principal que permite controlar sus elementos periféricos.

### Práctica 00

Se programó el LED que ya trae la placa en el pin 13 para que parpadee, encendiéndose y apagándose cada segundo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 01-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop()
{
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

### Práctica 01

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 01-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
}
```

### Práctica 02

Se probó la función delay, que marca cuánto tiempo se queda el LED encendido y apagado, usando un segundo de espera.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 03-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, LOW);
}
```

### Práctica 03

Se conectó un LED directamente al Arduino para que parpadee con el mismo código de las prácticas anteriores.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 04-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

### Práctica 04

Se armó el circuito en la protoboard con una resistencia que protege al LED, y se repitió el parpadeo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 05-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

### Práctica 05

Se agregó un segundo LED con su resistencia, y el código los hace prender uno después del otro.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 06-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

### Práctica 06

Con el mismo circuito de dos LEDs, el programa los enciende y apaga al mismo tiempo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 07-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

### Práctica 07

Se conectó un display de 7 segmentos y se enviaron señales HIGH y LOW a cada segmento para formar un número.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 08-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);
  pinMode(12, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(12, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(12, LOW);
  delay(1000); // Wait for 1000 millisecond(s)
}
```

### Práctica 08

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 9-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);	//Segmento e
  pinMode(12, OUTPUT);	//Segmento d
  pinMode(10, OUTPUT);	//Segmento c
  pinMode(9, OUTPUT);	//Segmento punto
  pinMode(7, OUTPUT);	//Segmento b
  pinMode(6, OUTPUT);	//Segmento a
  pinMode(5, OUTPUT);	//Segmento f
  pinMode(4, OUTPUT);	//Segmento g
}

void loop()
{
  digitalWrite(6, HIGH);//Segmento a
  digitalWrite(7, HIGH); //Segmento b
  digitalWrite(10, HIGH); //Segmento c
  digitalWrite(12, HIGH); //Segmento d
  digitalWrite(13, HIGH); //Segmento e
  digitalWrite(5, HIGH); //Segmento f
  digitalWrite(4, HIGH); //Segmento g
  digitalWrite(9, HIGH); //Segmento punto
  delay(1000);
}
```

### Práctica 09

Se usó un botón como entrada digital. Mientras lo presionas, el LED se enciende.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 10-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//
void setup()
{
  pinMode(13, OUTPUT);	//Segmento e
  pinMode(12, OUTPUT);	//Segmento d
  pinMode(10, OUTPUT);	//Segmento c
  pinMode(9, OUTPUT);	//Segmento punto
  pinMode(7, OUTPUT);	//Segmento b
  pinMode(6, OUTPUT);	//Segmento a
  pinMode(5, OUTPUT);	//Segmento f
  pinMode(4, OUTPUT);	//Segmento g
}

void loop()
{
    // Mostramos el numero 0
  digitalWrite(6, HIGH);//Segmento a
  digitalWrite(7, HIGH); //Segmento b
  digitalWrite(10, HIGH); //Segmento c
  digitalWrite(12, HIGH); //Segmento d
  digitalWrite(13, HIGH); //Segmento e
  digitalWrite(5, HIGH); //Segmento f
  digitalWrite(4, LOW); //Segmento g
  digitalWrite(9, LOW); //Segmento punto
  delay(1000);
  
    // Mostramos el numero 1
  digitalWrite(6, LOW);//Segmento a
  digitalWrite(7, HIGH); //Segmento b
  digitalWrite(10, HIGH); //Segmento c
  digitalWrite(12, LOW); //Segmento d
  digitalWrite(13, LOW); //Segmento e
  digitalWrite(5, LOW); //Segmento f
  digitalWrite(4, LOW); //Segmento g
  digitalWrite(9, LOW); //Segmento punto
  delay(1000);
  
    // Mostramos el numero 2
  digitalWrite(6, HIGH);//Segmento a
  digitalWrite(7, HIGH); //Segmento b
  digitalWrite(10, LOW); //Segmento c
  digitalWrite(12, HIGH); //Segmento d
  digitalWrite(13, HIGH); //Segmento e
  digitalWrite(5, LOW); //Segmento f
  digitalWrite(4, HIGH); //Segmento g
  digitalWrite(9, LOW); //Segmento punto
  delay(1000);
  
}
```

### Práctica 10

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 10-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//

void setup()
{
  pinMode(13, OUTPUT);	//LED
  
  pinMode(8, INPUT);	//BOTON
}

void loop()
{
  digitalWrite(13, digitalRead(8)); //Escribimpos en el LED el valor del BOTON
}
```

### Práctica 11

Se usó una condición if y else para leer el botón. Si está presionado se enciende el LED, y si no, se apaga.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 12-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//

void setup()
{
  pinMode(13, OUTPUT);	//LED1
  pinMode(8, INPUT);	//BOTON1
  
  pinMode(11, OUTPUT);	//LED2
  pinMode(2, INPUT);	//BOTON2
}

void loop()
{
  
  digitalWrite(13, digitalRead(8)); //Escribimpos en el LED1 el valor del BOTON1
  digitalWrite(11, digitalRead(2)); //Escribimpos en el LED2 el valor del BOTON2
}
```

### Práctica 12

Es lo mismo que la práctica 12, pero con dos botones y dos LEDs, cada botón controlando su LED.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 13-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//

void setup()
{
  pinMode(13, OUTPUT);	//LED
  
  pinMode(8, INPUT);	//BOTON
}

void loop()
{
  
  if (digitalRead(8) == HIGH)		//Pregunta si el boton1 esta activado
  {
    digitalWrite(13, HIGH);			//SI: encendemos el led1
  }
  else if(digitalRead(8) == LOW)	//Pregunta si el boton1 esta desactivado
  {
    digitalWrite(13, LOW);			//SI: apagamos el led1
  }
}
```

### Práctica 13

Se simuló una compuerta OR. El LED se enciende si se presiona un botón o los dos.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 14-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//

void setup()
{
  pinMode(13, OUTPUT);	//LED1
  pinMode(8, INPUT);	//BOTON1
  
  pinMode(11, OUTPUT);	//LED2
  pinMode(2, INPUT);	//BOTON2
}

void loop()
{
  
  if (digitalRead(8) == HIGH)		//Pregunta si el boton1 esta activado
  {
    digitalWrite(13, HIGH);			//SI: encendemos el led1
  }
  else if(digitalRead(8) == LOW)	//Pregunta si el boton1 esta desactivado
  {
    digitalWrite(13, LOW);			//SI: apagamos el led1
  }
  
  if (digitalRead(2) == HIGH)		//Pregunta si el boton2 esta activado
  {
    digitalWrite(11, HIGH);			//SI: encendemos el led2
  }
  else if(digitalRead(2) == LOW)	//Pregunta si el boton2 esta desactivado
  {
    digitalWrite(11, LOW);			//SI: apagamos el led2
  }
}
```

### Práctica 14

Se simuló una compuerta AND. El LED solo se enciende si se presionan los dos botones a la vez.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 15-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//

void setup()
{
  //Inicializamos puertos
  pinMode(13, OUTPUT);	//LED1
  
  pinMode(8, INPUT);	//BOTON1
  pinMode(2, INPUT);	//BOTON2
}

void loop()
  
{
  if (digitalRead(8) == HIGH || digitalRead(2) == HIGH)		//Pregunta si se cumple la condición
  {
    digitalWrite(13, HIGH);			//SI: encendemos el led1
  }
  else	//En caso contrario
  {
    digitalWrite(13, LOW);			//NO: apagamos el led1
  }

}
```

### Práctica 15

Se hizo un contador con varios LEDs. Cada vez que presionas el botón se enciende un LED más, y al llegar al máximo se reinicia.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 16-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
//

void setup()
{
  //Inicializamos puertos
  pinMode(13, OUTPUT);	//LED1
  
  pinMode(8, INPUT);	//BOTON1
  pinMode(2, INPUT);	//BOTON2
}

void loop()
{
  
  if (digitalRead(8) == HIGH && digitalRead(2) == HIGH)		//Pregunta si se cumple la condición
  {
    digitalWrite(13, HIGH);			//SI: encendemos el led1
  }
  else	//En caso contrario
  {
    digitalWrite(13, LOW);			//NO: apagamos el led1
  }

}
```

### Práctica 16

Se conectó un servomotor y se programó para que se coloque en una posición fija, 90 grados en el ejemplo de tu amigo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 17-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
// CONTADOR

int cuenta = 0;		//Variable que guarda el numero de veces que se ha contado

void setup()
{
  //Inicializamos puertos
  pinMode(13, OUTPUT);	//LED1
  pinMode(12, OUTPUT);	//LED2
  pinMode(11, OUTPUT);	//LED3
  pinMode(10, OUTPUT);	//LED4
  pinMode(2, INPUT);	//BOTON
}

void loop()
{
  if (digitalRead(2) == HIGH)		//Pregunta si el boton esta activado
  {
    cuenta++;
    delay(500);
  }
  if(cuenta >= 5)
  {
    cuenta = 0;
  }
  
  if(cuenta == 0)
  {
  	digitalWrite(13, LOW);
    digitalWrite(12, LOW);
    digitalWrite(11, LOW);
    digitalWrite(10, LOW);
  } 
  else if(cuenta == 1)
  {
  	digitalWrite(13, HIGH);
    digitalWrite(12, LOW);
    digitalWrite(11, LOW);
    digitalWrite(10, LOW);
  } 
  else if(cuenta == 2)
  {
  	digitalWrite(13, HIGH);
    digitalWrite(12, HIGH);
    digitalWrite(11, LOW);
    digitalWrite(10, LOW);
  }
  else if(cuenta == 3)
  {
  	digitalWrite(13, HIGH);
    digitalWrite(12, HIGH);
    digitalWrite(11, HIGH);
    digitalWrite(10, LOW);
  }
  else if(cuenta == 4)
  {
  	digitalWrite(13, HIGH);
    digitalWrite(12, HIGH);
    digitalWrite(11, HIGH);
    digitalWrite(10, HIGH);
  }
}
```

### Práctica 17

El servomotor recorre una secuencia de posiciones (0, 90 y 180 grados) con una pausa de un segundo entre cada una.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 18-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
// Incluímos la librería para poder controlar el servo
#include <Servo.h>

// Declaramos la variable para controlar el servo
Servo servoMotor;

void setup()
{
  // Iniciamos el servo para que empiece a trabajar con el pin 9
  servoMotor.attach(9);
}

void loop()
{
  // Desplazamos a la posición 0º
  servoMotor.write(0);
  // Esperamos 1 segundo
  delay(1000);
  
  // Desplazamos a la posición 90º
  servoMotor.write(90);
  // Esperamos 1 segundo
  delay(1000);
  
  // Desplazamos a la posición 180º
  servoMotor.write(180);
  // Esperamos 1 segundo
  delay(1000);
}
```

### Práctica 18

La posición del servomotor se controla con un potenciómetro. El código convierte la lectura analógica en un ángulo de 0 a 180 grados.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 19-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
// Incluímos la librería para poder controlar el servo
#include <Servo.h>

// Declaramos la variable para controlar el servo
Servo servoMotor;

void setup()
{
  // Iniciamos el servo para que empiece a trabajar con el pin 9
  servoMotor.attach(9);
}

void loop()
{
  // Desplazamos a la posición 0º
  servoMotor.write(0);
  // Esperamos 1 segundo
  delay(1000);
  
  // Desplazamos a la posición 90º
  servoMotor.write(90);
  // Esperamos 1 segundo
  delay(1000);
  
  // Desplazamos a la posición 180º
  servoMotor.write(180);
  // Esperamos 1 segundo
  delay(1000);
}
```

### Práctica 19 

Se agregó un segundo servomotor y ambos se mueven con un solo potenciómetro.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 19_2-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
// Incluímos la librería para poder controlar el servo
#include <Servo.h>

// Declaramos la variable para controlar el servo
Servo servoMotor;
int valor;		//variable que almacena la lectura analógica raw
int pos;        //Variable que almacena la posicion del servo

void setup()
{
  // Iniciamos el servo para que empiece a trabajar con el pin 9
  servoMotor.attach(9);
}

void loop()
{
  // leemos del pin A0 valor
  valor = analogRead(A0);
  //Convertimos el valor del potenciometro a una 
  //que entienda el servo
  pos = map(valor, 0, 1023, 0, 180);
  //Mandamos la posicion al servo 
  servoMotor.write(pos);
  // Esperamos 1 segundo
  delay(1000);
}
```

### Práctica 19 - Parte 2

Cada servomotor tiene su propio potenciómetro, así que se mueven de forma independiente.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 20-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
#include <Servo.h>
int valor;		//variable que almacena la lectura analógica raw
int pos;        //Variable que almacena la posicion del servo


//Le decimos al codigo que va a existir un servo
//llamado my servo
Servo myservo1;
Servo myservo2;

void setup()
{
  //Le decimos al codigo donde esta conectado el servo 1
  myservo1.attach(9);
  //Le decimos al codigo donde esta conectado el servo 2
  myservo2.attach(2);
}

void loop()
{
  // leemos el valor de potenciometro
  valor = analogRead(A0);
  //Convertimos el valor del potenciometro a una 
  //que entienda el servo
  pos = map(valor, 0, 1023, 0, 180);
  //Mandamos la posicion al servo 1
  myservo1.write(pos);
  //Mandamos la posicion al servo 2
  myservo2.write(pos);
  //esperamos un poco para que se mueva
  delay(10);
}
```

### Práctica 20 

Segunda grabación del mismo circuito, mostrando con más detalle el movimiento independiente de cada servo.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 20_2-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
#include <Servo.h>
int valor1;		//variable que almacena la 
				//lectura analógica1
int valor2;		//variable que almacena la 
				//lectura analógica2
int pos1;        //Variable que almacena la posicion del servo1
int pos2;        //Variable que almacena la posicion del servo2


//Le decimos al codigo que va a existir un servo
//llamado my servo
Servo myservo1;
Servo myservo2;

void setup()
{
  //Le decimos al codigo donde esta conectado el servo 1
  myservo1.attach(9);
  //Le decimos al codigo donde esta conectado el servo 2
  myservo2.attach(2);
}

void loop()
{
  // leemos el valor de potenciometro1
  valor1 = analogRead(A0);
  // leemos el valor de potenciometro2
  valor2 = analogRead(A1);
  //Convertimos el valor del potenciometro a una 
  //que entienda el servo
  pos1 = map(valor1, 0, 1023, 0, 180);
  pos2 = map(valor2, 0, 1023, 0, 180);
  //Mandamos la posicion al servo 1
  myservo1.write(pos1);
  //Mandamos la posicion al servo 2
  myservo2.write(pos2);
  //esperamos un poco para que se mueva
  delay(10);
}
```

### Práctica 21

El servomotor se alimenta con una fuente externa en lugar del Arduino, para darle la potencia que necesita.

<video muted controls width="600">
  <source src="{{ '/assets/img/03-videos/practica 21-converted.mp4' | relative_url }}" type="video/mp4">
</video>

```cpp
// C++ code
#include <Servo.h>
int valor;		//variable que almacena la lectura analógica raw
int pos;        //Variable que almacena la posicion del servo


//Le decimos al codigo que va a existir un servo
//llamado my servo
Servo myservo1;
Servo myservo2;

void setup()
{
  //Le decimos al codigo donde esta conectado el servo 1
  myservo1.attach(9);
  //Le decimos al codigo donde esta conectado el servo 2
  myservo2.attach(2);
}

void loop()
{
  // leemos el valor de potenciometro
  valor = analogRead(A0);
  //Convertimos el valor del potenciometro a una 
  //que entienda el servo
  pos = map(valor, 0, 1023, 0, 180);
  //Mandamos la posicion al servo 1
  myservo1.write(pos);
  //Mandamos la posicion al servo 2
  myservo2.write(pos);
  //esperamos un poco para que se mueva
  delay(10);
}
```

