# Eliptic Curve Cryptography (ECC) (WIP)

with a 256-bit EC key have the same security level as a 3072-bit RSA key

everal operations using those keys (including signing) can be more efficient both time- and memory-wise

asymmetric cryptographic protocol that, like RSA and Diffie-Hellman (DH), relies on a trapdoor function

rapdoor functions allow a client to keep data secret by performing a mathematical operation which is computationally easy to do, but currently understood to be very expensive to undo.

Conics, which are given by equations where each term has combined degree at most two, such as&#x20;

X^2 + 2X Y + 4Y^2 = 3

, are more complex, but are still well-understood. In fact, it can be shown that in the real projective plane, every conic can be affinely transformed into one of the following five curves:

1. &#x20;: a double line
2. &#x20;: a single point
3. &#x20;: two lines
4. &#x20;: the empty set
5. &#x20;: a unit circle

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Una curva elítica se representa como E:y2=X3+aX+b conocido como ecuacion de Weierstrass, y la curva es todas las posibles soluciones a dicha ecuacion.

Esto tambien puede entenderswe como E(Fp)={(x,y):x,y∈Fp satisfying y2=x3+ax+b}∪O

Podemos definir un operador que llamaremos "suma de puntos". Este operador toma dos puntos de una curva y produce un tercero. Esta es una operacion de un grupo abeliano (las soluciones de la ecuacion)

The point O acts as the identity operator of the group: P + O = P and P + ( − P )=O, y cumple con associatividad y comutatividad

Tambien debe satisfacerce 4a3+27b2=/0 para que no haya <mark style="color:red;">singularidades?</mark>



P y Q son puntos con coordenadas x y y  ambos ubicados en la Curva, si se traza una linea recta entro los dos puntos podemos tener los siguientes caso

Asi mismo podemos entender la multiplicación escalar de un punto como la suma repetida de puntos del mismo

Q=\[ 2 ] P=P+P  Resulta que la multiplicación escalar es una función trampa. El ECC se basa en la dificultad de encontrar la n tal que Q\[n] = P dado Q y P

reflect it along the y y direction to produce R ′R ( x , − y ). The result of the point addition is P+ Q =R ′

<figure><img src="../../.gitbook/assets/image (927).png" alt=""><figcaption></figcaption></figure>

* Caso 1: La linea intercepta en un tercer punto la curva, R es el valor de intercepto
* Caso 2: La linea no intercepta una tercera vez, las 4 coordenadas de los puntos son diferentes
* Caso 3:  La coordena x de P y Q es la mismo
* Caso 4: la linea solo toma una tangente sobre la curva entera

## Operaciones

<figure><img src="../../.gitbook/assets/image (924).png" alt=""><figcaption></figcaption></figure>

Para hallar valores nP hacemos el metodo de duplicar y sumar, encontrar la potencia de 2 mas cercana y luego rellenar con potencias de 2 hasta alcanzar el numero

Para hallar el inverso de un punto P, we do -P = (x, -(y mod n))

