---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Pwn (WIP)

## Binario

Archivo ejecutable que puede ser entendido por el sistema operativo

Lenguaje Compilado vs Interpretado

## Arquitecturas

32 bits  cada valor hexadecimal representa 4 bits | los valors de la stack empiezan por R ejemplo RIP. Se representa como x86\
64 bits, tenemos la posibilidad de representar mas valores | los valores de la stack empiezan por E ejemplo RIP. Se representa como x64

## Endianess&#x20;

Big Endian manera de almacenar valor del byte mas significativo al menos (izquierda a derecha, intuitivo a lectura humana)\
Little Endian los pares hexadecimales se representan de derecha a izquierda (no intuitivo)

## Segmentos del binario

Encabezado: Headers\
Codigo: Logica de instrucciones de lo que se va a ejecutar\
Data: Donde se guardan las variables\
Pila: Estructura de datos que almacena los valores de las instrucciones \
Heap: Crece para no colapsar y ocupar la \
Symbols\
Imports (Librerias)

7ffff7 representar encabezados\
5555 dentro del binario\
7ffffff posicion del stack

## Stack

Esta es de tamaño fijo. comienza en una posicion de memoria alta y empieza a bajar (crece hacia abajo)\
EBP donde esta mi stack, la base\
EIP a donde va la siguiente instruccion\
ESP donde es el limite de mi stack

## Heap

Esta es de tamaño dinamica para almacenar variables persistentes\
Crece exponencialmente cada que llega al limite de su espacio

## Libreria C

Funciones estandar del sistema operativo para conectar las funciones con los ejecutables

## PLT (Procedure Linkage Table)

eTiene informacion de si es la primera vez que llama una funcion para sino buscarlas en Libc. Se la pasa a GOT para que la recuerde

## GOT&#x20;

Almacena las llamadas a funciones que se han llamado previa



## <mark style="color:red;">Assembly</mark>

Lenguaje de bajo nivel, utiliza directablente&#x20;

### Registros

Son cajas de memoria que guardan variables\
Proposito general: Guardar lo que sea\
Proposito especial: funciones especificas como los punteros de la stack\
\
Pueden ser de \
R para 64 bits\
R de 32&#x20;

### Mnemonicos

Palabras clave para dar las instrucciones de lo que se debe hacer\
De derehca izquierda, lo que se opere termina en la variable de la izquierda\
Syscall: Funciones especificas a las que se les pasa valores en registros especiales especificos para su funcionamiento\
x86.syscall.sh



xor rsi,rsi --> hacer \


## <mark style="color:red;">PWN</mark>

protecciones\
NX — evita ejecutar codigo shellcodeen stack o heap\
Canary — Evita sobreescritura del retorno, compara un valor aleatorio y si ha cambiado no deja que se ejecute el binario, evita bufferoverflow\
PIE — Aleatoriza las posiciones de memoria, excepto las ultimas 3\
RELRO — Proteger la GOT de sobreescritura\
ASLR — Aleatoriza las posiciones de memoria a nivel de kernel

## Practica

herramientas [https://github.com/apogiatzis/gdb-peda-pwndbg-gef](https://github.com/apogiatzis/gdb-peda-pwndbg-gef)

{% embed url="https://ropemporium.com/" %}

