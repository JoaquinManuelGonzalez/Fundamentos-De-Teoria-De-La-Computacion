# Trabajo Práctico Nro 1 - La Máquina de Turing

## Ejercicio 1
Responder breve y claramente los siguientes incisos:

1. ¿En qué se diferencia un problema de búsqueda de un problema de decisión?

- La diferencia es que un **problema de búsqueda** consiste en encontrar una solución a una instancia dada del problema a resolver, la máquina puede devolver una solución al problema o en el caso que no exista una solución devolver "no". Mientras que un **problema de decisión** consiste en determinar la existencia de una solución a un problema, siendo las salidas posibles "si" o "no".

2. ¿Por  qué  en  el  caso  de  los  problemas  de  decisión,  podemos  referirnos  indistintamente  a problemas y lenguajes?

- Podemos referirnos indistintamente a problemas y lenguajes porque existe una **correspondencia directa y natural entre un problema de decisión y el lenguaje que representa sus instancias positivas**
    - Un problema de decisión es aquel cuya respuesta para cualquier instancia es "si" o "no".
    - Un lenguaje, en la teoría de la computación, es un conjunto de cadenas formadas a partir de un alfabeto.
    - Para un problema de decisión dado, podemos definir un lenguaje que contenga todas las cadenas que representan las instancias para las cuales la respuesta al problema es "sí". Estas son las instancias positivas del problema.
    - Una Máquina de Turing (MT) que resuelve un problema de decisión se comporta como un reconocedor de lenguajes. Cuando se le proporciona una cadena de entrada (que representa una instancia del problema):
        - Si la respuesta al problema para esa instancia es "sí", la MT acepta la cadena.
        - Si la respuesta es "no", la MT rechaza la cadena.
    - Por lo tanto, el lenguaje aceptado por la MT es precisamente el conjunto de todas las cadenas que corresponden a las instancias positivas del problema de decisión.

3. El problema de satisfactibilidad de las fórmulas booleanas, en su forma de decisión, es: “Dada una  fórmula  φ,  ¿existe  una  asignación  A  de  valores  de  verdad  que  la  hace  verdadera?” Enunciar el problema de búsqueda asociado.

- **Problema de Búsqueda:** "Dada una fórmula booleana φ, encontrar, si existe, una asignación A de valores de verdad a las variables de φ que haga que la evaluación de φ con A sea verdadera."

4. Otra visión de MT es la que genera un lenguaje (visión generadora). En el caso del problema del  inciso  anterior,  ¿qué  lenguaje  generaría  la  MT  de  visión  generadora  que  resuelve  el problema?

- Para el problema de las fórmulas boolenas satisfactibles, el lenguaje que generaría una MT con visión generadora sería **el cojunto de representaciones (cadenas) de todas las fórmulas booleanas que son satisfactibles.** Podría tener la forma: L(M) = {φ1, φ2, φ3, …}, donde φi es una fórmula booleana satisfactible.

5. ¿Qué postula la Tesis de Church-Turing?

- La Tesis de Church-Turing postula que **todo dispositivo computacional físicamente realizable puede ser simulado por una Máquina de Turing (MT).** En otras palabras, la tesis afirma que cualquier proceso que pueda ser considerado como un algoritmo o un método efectivo de cálculo puede ser llevado a cabo por una Máquina de Turing. A pesar de su simplicidad, la Máquina de Turing se considera un modelo computacional suficientemente poderoso como para simular cualquier otra forma concebible de computación.

6. ¿Cuándo dos MT son equivalentes? ¿Y cuándo dos modelos de MT son equivalentes?

- Dos **MT son equivalentes** si aceptan el mismo lenguaje (es decir, si resuelven el mismo problema). **Dos modelos de MT son equivalentes** si dada una MT de un modelo existe una MT equivalente del otro.

---

## Ejercicio 2
Dado el alfabeto Ʃ = {0, 1}:

1. Obtener el conjunto Ʃ* y el lenguaje incluido en Ʃ* con cadenas de a lo sumo 2 símbolos.

- Ʃ* = {λ, 0, 1, 00, 01, 10, 11, 000, 001, 010, 011, 100, 101, 110, 111, ...}
- L = {λ, 0, 1, 00, 01, 10, 11}

2. Sea el lenguaje L = {0^n^1^n^ | n ≥ 0}. Obtener los lenguajes Ʃ* ⋂ L, Ʃ* ⋃ L y L^C^ respecto de Ʃ*.

- Ʃ* ⋂ L = L
- Ʃ* ⋃ L = Ʃ*
- L^C^ = Ʃ* - L

---

## Ejercicio 3
En clase se mostró una MT no determinística (MTN) que acepta las cadenas de la forma ha^n^ o hb^n^, con n ≥ 0. Construir (describir la función de transición) una MT  determinística (MTD) equivalente.

- **Idea General:**
    - Recorrer la cadena y determinar si después de "h" hay una "a" o una "b".
        - Si hay una "a" luego de "h" buscamos solo "a" recorriendo hacia la derecha, si encontramos una "b" frenamos y retornamos "no".
        - Si hay una "b" luego de "h" buscamos solo "b" recorriendo hacia la derecha, si encontramos una "a" frenamos y retornamos "no".
        - Si recorremos toda la cadena retornamos "si".

- **Estados:** Q = {q~0~, q~1~, q~a~, q~b~, q~A~, q~R~}
1. q~0~: Estado inicial.
2. q~1~: M determina que letra hay.
3. q~a~: M busca una "a".
4. q~b~: M busca una "b".

- **Alfabeto:** Γ = {h, a, b, B}

- **Función de Transición:** δ
1. δ(q~0~, h) = {(q~1~, h, R)} → Pasamos a determinar que letra hay despúes.
2. δ(q~1~, a) = {(q~a~, a, R)} → Encontramos "a" y buscamos más "a".
3. δ(q~1~, b) = {(q~b~, b, R)} → Encontramos "b" y buscamos más "b".
4. δ(q~1~, B) = {(q~A~, B, S)} → Encontramos B y aceptamos.
5. δ(q~a~, a) = {(q~a~, a, R)} → Recorremos siguiendo con las "a".
6. δ(q~a~, B) = {(q~A~, B, S)} → Llegamos al final y solo había "a".
7. δ(q~b~, b) = {(q~b~, b, R)} → Recorremos siguiendo con las "b".
8. δ(q~b~, B) = {(q~A~, B, S)} → Llegamos al final y solo había "b".

- **MT M = (Q, Γ, δ, q~0~, q~A~, q~R~)**

---

## Ejercicio 4
Describir la idea general de una MT con varias cintas que acepte, de la manera más eficiente posible (menor cantidad de pasos), el lenguaje L = {a^n^b^n^c^n^ | n ≥ 0}.

- **Idea General:**
    - La MT va a utilizar 2 cintas:
        - La primera va a ser utilizada como cinta de entrada de los datos, por ejm. contendría los vaslores (a, a, a, b, b, b, c, c, c).
        - La segunda va a ser utilizada como una cinta contadora que nos permita llevar un conteo de la cantidad de "a", "b" y "c" que tiene la cadena de la cinta de entrada.
    - Si la primera cinta está vacía, es decir, es B, devolvemos "si".
    - Si en la primera cinta no encontramos una "a" en primer lugar, devolvemos "no".
    - Suponiendo que en la primera cinta nos encontramos con una "a" en primer lugar y la segunda estará B, en ese caso marcamos en la segunda cinta que hay una "a" y avanzamos los 2 cabezales de la cintas hacia la derecha, acá nos podemos encontrar 3 casos:
        - La letra que sigue es una "a", en ese caso marcamos que hay una "a" en la segunda cinta y avanzamos los 2 cabezales hacia la derecha.
        - La letra que sigue es una "b", en ese caso mantenemos el cabezal de la primera cinta en la posición actual (primera "b") y movemos el cabezal de la segunda cinta hacia la izquierda para que quede posicionado en la última "a" contada.
        - La letra que sigue es una "c" o encontramos un B, devolvemos "no".
    - Una vez empezamos a contabilizar las "b" recorriendo la primera cinta hacia la derecha y la segunda hacia la izquierda pueden pasar 5 casos:
        - La letra que sigue es una "b" en la primera cinta y en la segunda no hay B, en ese caso movemos el cabezal de la primera cinta hacia la derecha y el de la segunda cinta hacia la izquierda.
        - La letra que sigue es una "c" en la primera cinta y en la segunda hay B, en ese caso mantenemos el cabezal de la primera cinta en la posición actual (primera "c") y movemos el cabezal de la segunda cinta hacia la derecha para que quede posicionado en la primera "a" contada.
        - La letra que sigue es una "a" o encontramos un B en la primera cinta, devolvemos "no".
        - La letra que sigue es una "b" en la primera cinta pero en la segunda hay un B, devolvemos "no" ya que en ese caso la cantidad de "a" y "b" no serían las mismas.
        - La letra que sigue es B en la primera cinta y en la segunda no es B, devolvemos "no".
    - Una vez que empezamos a contabilizar las "c" recorriendo las 2 cintas hacia la derecha pueden pasar 5 casos:
        - La letra que sigue es una "c" en la primera cinta y en la segunda no hay B, en ese caso movemos los 2 cabezales hacia la derecha.
        - La letra que sigue es una "a" o una "b" en la primera cinta, devolvemos "no".
        - La letra que sigue es B en la primera cinta y en la segunda no es B, devolvemos "no".
        - La letra que sigue es B en las 2 cintas, devolvemos "si".
        - La letra que sigue es "c" en la primera cinta y en la segunda hay B, devolvemos "no" ya que en ese caso la cantidad de "a", "b" y "c" no serían las mismas.

---

## Ejercicio 5
Explicar  cómo  una  MT  sin  el  movimiento  S  (el  no  movimiento)  puede  simular (ejecutar) otra que sí lo tiene.

- Se podría simular haciendo que la MT cuando se llegue por ejm. al elemento en el que se quiera frenar mueva su cabezal hacia la izquierda y luego hacia la derecha, cambiando a un nuevo estado al moverse a la izquierda para garantizar el movimiento a la derecha sin hacer nada.

---

## Ejercicio 6
En clase se construyó una MT con 2 cintas que acepta L = {w | w ∈ {a, b}* y w es un palíndromo}. Construir  una  MT  equivalente  con  1  cinta.  *Ayuda:  la  solución  que  vimos  para aceptar el lenguaje de las cadenas a^n^b^n^, con n ≥ 1, puede ser un buen punto de partida.*

- **Idea General:**
    - Recorrer la cadena haciendo una "ida y vuelta" marcando la primera letra y avazando hacia la derecha hasta la última, si la última letra es igual a la primera que encontramos, la marcamos y retrocedemos hacia la izquierda hasta chocarnos con la siguiente letra sin marcar y repetimos el proceso.
    - Cuando tenemos elementos marcados hacia nuestra derecha y hacia nuestra izquierda eso significa que la cadena es un palíndromo.

- **Estados:** Q = {q~0z~, q~0d~, , q~baf~, q~bai~, q~caf~, q~cai~, q~bbf~, q~bbi~, q~cbf~, q~cbi~, q~A~, q~R~}
1. q~0z~: Estado inicial de izquierda a derecha.
2. q~0d~: Estado inicial de derecha a izquierda.
3. q~baf~: Estado "Buscar A al Final".
4. q~bai~: Estado "Buscar A al Inicio".
5. q~caf~: Estado "Chequeo de A al Final".
6. q~cai~: Estado "Chequeo de A al Inicio".
7. q~bbf~: Estado "Buscar B al Final".
8. q~bbi~: Estado "Buscar B al Inicio".
9. q~cbf~: Estado "Chequeo de B al Final".
10. q~cbi~: Estado "Chequeo de B al Inicio".

- **Alfabeto:** Γ = {a, b, B}

- **Función de Transición:** δ
1. δ(q~0z~, a) = {(q~baf~, B, R)} → Iniciamos de izquierda a derecha con "a"
2. δ(q~0z~, b) = {(q~bbf~, B, R)} → Iniciamos de izquierda a derecha con "b"
3. δ(q~baf~, a) = {(q~baf~, a, R)} → Buscamos "a" al final y encontramos "a" en el camino
4. δ(q~baf~, b) = {(q~baf~, b, R)} → Buscamos "a" al final y encontramos "b" en el camino
5. δ(q~baf~, B) = {(q~caf-, B, L)} → Buscamos "a" al final y encontramos B en el camino
6. δ(q~caf~, a) = {(q~0d~, B, L)} → Chequeamos si la letra es una "a" al final
7. δ(q~caf~, B) = {(q~A~, B, S)} → Nos damos cuenta que la cadena es un palíndromo
8. δ(q~0d~, a) = {(q~bai~, B, L)} → Iniciamos de derecha a izquierda con "a"
9. δ(q~0d~, b) = {(q~bbi~, B, L)} → Iniciamos de derecha a izquierda con "b"
10. δ(q~bai~, a) = {(q~bai~, a, L)} → Buscamos "a" al inicio y encontramos "a" en el camino 
11. δ(q~bai~, b) = {(q~bai~, b, L)} → Buscamos "b" al inicio y encontramos "b" en el camino
12. δ(q~bai~, B) = {(q~cai-, B, R)} → Buscamos "a" al inicio y encontramos B en el camino
13. δ(q~cai~, a) = {(q~0z~, B, R)} → Chequeamos si la letra es una "a" al inicio
14. δ(q~cai~, B) = {(q~A~, B, S)} → Nos damos cuenta que la cadena es un palíndromo
15. δ(q~bbf~, a) = {(q~bbf~, a, R)} → Buscamos "b" al final y encontramos "a" en el camino
16. δ(q~bbf~, b) = {(q~bbf~, b, R)} → Buscamos "b" al final y encontramos "b" en el camino
17. δ(q~bbf~, B) = {(q~cbf-, B, L)} → Buscamos "b" al final y encontramos B en el camino
18. δ(q~cbf~, b) = {(q~0d~, B, L)} → Chequeamos si la letra es una "b" al final
19. δ(q~cbf~, B) = {(q~A~, B, S)} → Nos damos cuenta que la cadena es un palíndromo
20. δ(q~bbi~, a) = {(q~bbi~, a, L)} → Buscamos "b" al inicio y encontramos "a" en el camino
21. δ(q~bbi~, b) = {(q~bbi~, b, L)} → Buscamos "b" al inicio y encontramos "b" en el camino
22. δ(q~bbi~, B) = {(q~cbi-, B, R)} → Buscamos "b" al inicio y encontramos B en el camino
23. δ(q~cbi~, b) = {(q~0z~, B, R)} → Chequeamos si la letra es una "b" al inicio
24. δ(q~cbi~, B) = {(q~A~, B, S)} → Nos damos cuenta que la cadena es un palíndromo

- **MT M = (Q, Γ, δ, q~0z~, q~A~, q~R~)**

---

## Ejercicio 7
Construir una MT que calcule la resta de dos números. *Ayuda: se puede considerar la idea de solución propuesta en clase. ACLARACIÓN: Tomo las precondiciones que se muestran en la clase, los números están codificados en unario, separados por un 0 y las restas dan resultasdos >= 0*

- **Idea General para solución con 2 cintas:**
    - En la primera cinta vamos a tener la resta codificada en unario, por ejm. la resta 4 - 3 sería (11110111).
    - En la segunda cinta lo que vamos a hacer es ir copiando hacia la derecha el primer número a restar y cuando lleguemos al inicio del segundo número iremos tachando hacia la izquierda el primer número copiado, lo que quede en la segunda cinta será el resultado a devolver.

- **Estados:** Q = {q~0~, q~copiar~, q~restar~, q~A~, q~R~}
1. q~0~: Estado inicial.
2. q~copiar~: Estado para copiar el primer número.
3. q~restar~: Estado para ir restando en la segunda cinta.

- **Alfabeto:** Γ = {0, 1, B}

- **Función de Transición:** δ
1. δ(q~0~, 1, B) = {(q~copiar~, (1, R), (1, R))} → Empezamos a copiar el primer número
2. δ(q~copiar~, 1, B) = {(q~copiar~, (1, R), (1, R))} → Recorremos el primer número y copiamos
3. δ(q~copiar~, 0, B) = {(q~restar~, (0, R), (B, L))} → Llegamos al final del primer número
4. δ(q~restar~, 1, 1) = {(q~restar, (1, R), (0, L))} → Tachamos en la segunda cinta
5. δ(q~restar~, B, 1) = {(q~A~, (B, S), (1, S))} → Terminamos el segundo número y este era más chico
6. δ(q~restar~, B, B) = {(q~A~, (B, S), (B, S))} → Terminamos el segundo número y la resta es 0

- **MT M = (Q, Γ, δ, q~0~, q~A~, q~R~)**

---

## Ejercicio 8
Construir una MT que genere todas las cadenas de la forma a^n^b^n^, con n ≥ 1. *Ayuda: se puede considerar la idea de solución propuesta en clase.*

- **Idea General para solución con 2 cintas:**
    - En la primera cinta vamos a tener todas las cadenas (ab, aabb, aaabbb, aaaabbbb, ...).
    - La segunda cinta la vamos a usar como un contador para ir viendo la cantidad de "a" y de "b" que tenemos que ir poniendo en la primera cinta.

- **Estados:** Q = {q~0~, q~a~, q~b~, q~A~, q~R~}
1. q~0~: Estado inicial.
2. q~a~: Estado para escribir una "a".
3. q~b~: Estado para escribir una "b" y delimitar con ",".

- **Alfabeto:** Γ = {a, b, ",", B}

- **Función de Transición:** δ
1. δ(q~0~, B, B) = {(q~a~, (B, S), (1, S))} → Preparamos el contador de la segunda cinta
2. δ(q~a~, B, 1) = {(q~a~, (a, R), (1, R))} → Copiamos una "a" en la primera cinta
3. δ(q~a~, B, B) = {(q~b~, (B, S), (B, L))} → Preparamos las cintas para copiar las "b"
4. δ(q~b~, B, 1) = {(q~b~, (b, R), (1, L))} → Copiamos una "b" en la primera cinta
5. δ(q~b~, B, B) = {(q~a~, (",", R), (1, S))} → Delimitamos el fin de la cadena a^n^b^n^ y preparamos las cintas para copiar las "a"

- **MT M = (Q, Γ, δ, q~0~, q~A~, q~R~)**