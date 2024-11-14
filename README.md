# Controladores por Retroalimentación de Estados

## Controlabilidad y Observabilidad

*Controlabilidad*  
La controlabilidad se refiere a la capacidad de un sistema para ser manipulado o dirigido a cualquier estado deseado, utilizando el control adecuado.

Un sistema es controlable en un tiempo $$\( t_0 \)$$ si, desde cualquier estado inicial $$\( x(t_0) \)$$, se puede transferir a cualquier otro estado en un intervalo de tiempo finito.
  

#### Matriz de Controlabilidad

En sistemas discretos, el comportamiento del sistema es:

$$\[
x(k+1) = A x(k) + B u(k)
\]$$
$$\[
y(k) = C x(k) + D u(k)
\]$$

Donde:

$$\( x(k) \)$$ es el vector de estado en el tiempo $$\( k \)$$,

$$\( u(k) \)$$ es el vector de control en el tiempo $$\( k \)$$,

$$\( y(k) \$$) es la salida en el tiempo $$\( k \)$$,

$$\( A \)$$, $$\( B \)$$, y $$\( C \)$$ son matrices del sistema.

La matriz de controlabilidad se construye:

$$U=\left[ B,AB,A^{2}B,A^{3}B....A^{n-1}B \right]$$

Si el sistema es controlable, entonces el rango de la matriz de controlabilidad debe ser igual al número de variables de estado $$\( n \)$$ y el determinante de esta matriz debe ser diferente de cero. En otras palabras, si el sistema es controlable, el rango de U es igual a n.

💡 Ejemplo

A=[1.5,1/1,0]

B=[1/0]

y=[2,-1]



Queremos verificar si el sistema es controlable.

La matriz de controlabilidad  es:

U=[B,AB]

AB=[1.5,1/1,0][1/0]=[1.5/1]


U=[1,1.5/0,1]

Determinante de la matriz de controlabilidad

U=[1,1.5/0,1]=1


El determinante es 1, lo que es diferente de cero, lo que implica que el sistema es *controlable*.



*Observabilidad*

Se dice que un sistema es observable en el tiempo %%\( t_0 \)%% si, con el sistema en el estado $$X(t_{0})$$, es posible determinar dicho estado observando la salida durante un intervalo de tiempo finito.

En otras palabras, la observabilidad nos permite estimar cualquier variable de estado del sistema si conocemos sus entradas y salidas durante un período de tiempo. Esta propiedad es fundamental en el diseño de sistemas de control, como los controladores por retroalimentación de estados, ya que nos permite diseñar estimadores de estados cuando los estados no son directamente medibles.


#### Matriz de Observabilidad


V=[C/CA/CA^{2}...CA^{n-1}]

Donde n es el número de estados en el sistema.su determinante debe ser diferente de cero) para que el sistema sea observable.

 Si el rango de la matriz de observabilidad es igual al número de estados del sistema, entonces el sistema es observable.



💡 Ejemplo

se tiene un sistema con dos variables de estado y las siguientes matrices:


A=[1.5,1/1,0]

C=[2,-1]

la matriz de observabilidad es:

v=[C/CA]

CA=[2,-1][1.5,1/1,0]=[2,2]

V=[2,-1/2,2]

Determinante de la matriz de observabilidad

V=[2,-1/2,2]=6


 *el sistema es observable*.

### ¿Para qué sirven las condiciones de Controlabilidad y Observabilidad?

Las condiciones de controlabilidad y observabilidad son fundamentales en el diseño y análisis de sistemas de control. Estas condiciones no solo determinan si un sistema es manipulable o si sus estados pueden ser estimados con precisión, sino que también garantizan la existencia de soluciones factibles para los problemas de control.



## Control por retroalimentacion de estados



### *Control por Retroalimentación de Estados*


El objetivo principal de esta estrategia es asignar los polos del sistema en lazo cerrado de forma arbitraria mediante la matriz de ganancias  K . Esto implica que se puede modificar el comportamiento dinámico del sistema (en términos de su estabilidad y respuesta) ajustando los valores de  K  de manera que los polos del sistema cerrado estén ubicados en posiciones deseadas en el plano complejo.

u(k)=-k*x(k)


### Metodología de Diseño de Control por Retroalimentación de Estados

Para diseñar un controlador de retroalimentación de estados, se sigue un proceso estructurado:

1. Comprobar la controlabilidad del sistema
2. Determinar los coeficientes del polinomio característico del sistema en lazo abierto:
   - El polinomio característico de un sistema es el determinante de $$\( ZI - A \)$$, donde  A  es la matriz del sistema. Este polinomio tiene la forma:
     \[
     $$\|ZI - A |= Z^n + a_1 Z^{n-1} + \dots + a_n
     \]$$
   
3. Determinar La matriz T.Se utiliza para transformar el sistema en forma canónica controlable. Si el sistema está en esta forma, entonces  T  será la matriz identidad  I . Si no,  T  se calcula a partir de la matriz de controlabilidad U y la matriz  W (T=UW).

4. Determinar el polinomio deseado. Este polinomio se obtiene a partir de la ubicación de los polos deseados. Por ejemplo, si queremos que los polos estén en \( z = -0.2 + j0.4 \), \( z = -0.2 - j0.4 \), y \( z = -0.02 \), podemos construir el polinomio deseado en lazo cerrado.

5. Calcular las ganancias de retroalimentación de estados. Las ganancias  K  se calculan resolviendo la diferencia entre el polinomio característico del sistema y el polinomio deseado. Las ganancias de retroalimentación de estados  K se pueden obtener usando la fórmula:
     $$\[
     K = [\alpha_n - a_n, \alpha_{n-1} - a_{n-1}, \dots, \alpha_1 - a_1] \cdot T^{-1}
     \]$$
     donde $$\( \alpha_i \)$$ son los coeficientes del polinomio deseado y $$\( a_i \)$$ los del polinomio del sistema.



💡 Ejemplo

Consideremos un sistema con las siguientes matrices:

A=[0,1,0/0,0,1/-1,-5,-6]

B=[0/0/1]

Queremos diseñar un controlador que ubique los polos del sistema cerrado en las siguientes posiciones:

z = -0.2 + j0.4

z = -0.2 - j0.4

z = -0.02


#### Comprobación de Controlabilidad

La matriz de controlabilidad  se calcula como:

$$U=[B,AB,A^2B]$$


La matriz de controlabilidad U es:

U=[0,0,1/0,1,-6/1,-6,31]

 el sistema es controlable.


#### Determinar el Polinomio Característico en Lazo Abierto

El polinomio característico del sistema se obtiene como:

$$\[
P(Z) = |ZI - A| = Z^3 + Z^2 + 5Z + 1
\]$$

Este es el polinomio característico en lazo abierto

#### Determinar la Matriz  T 

La matriz T  se construye usando los coeficientes del polinomio característico y la matriz de controlabilidad. Para este caso,  T  se construye con los coeficientes  a_1 = 6 ,  a_2 = 5 , y  a_3 = 1 .

W=[5,6,1/6,1,0/1,0,0]

T=I=[1,0,0/0,1,0/0,0,1]

#### Determinar el Polinomio Deseado

El polinomio deseado para el sistema cerrado con los polos en las ubicaciones deseadas 

$$\[
P_d(Z) = (Z + 0.2 - j0.4)(Z + 0.2 + j0.4)(Z + 0.02)
\]$$


$$\[
P_d(Z) = Z^3 + 0.402Z^2 + 0.2008Z + 0.0004
\]$$

#### Calcular las Ganancias de Retroalimentación de Estados**



$$\[
K = [\alpha_n - a_n, \alpha_{n-1} - a_{n-1}, \dots, \alpha_1 - a_1] \cdot T^{-1}
\]$$

Sustituyendo los coeficientes $$\( \alpha_i \$$ del polinomio deseado y los coeficientes $$\( a_i \)$$ del polinomio del sistema:

K=[0.0004-1,0.2008-5,0.402-6]=[-0.996,-4.799,-5.598]




# Ejercicios#

📚 Ejercicio 1:

tenemos el siguiente sistema:

A=[0,1,0/0,0,1/-3,-4,-5]

B=[0/0/1]


se tienen los siguentes polos

z = -1 

 z = -2
 
 z = -3 + j
 
 z = -3 - j
 

### *Paso 1: Comprobación de Controlabilidad*

La matriz de controlabilidad  U  se forma como:
$$\[
U = [B, AB, A^2B]
\]$$

Calculamos  AB :

AB=[0,1,0/0,0,1/-3,-4,-5][0/0/1]=[0,1,-5]

Se calcula $$\( A^2B \)$$

$$A^2B=[0,1,0/0,0,1/-3,-4,-5]^2[0/0/1]$$

$$A^2=[0,0,1/-3,-4,-5/15,17,21]$$

$$A^2B[[0,0,1/-3,-4,-5/15,17,21][0/0/1]=[1/-5/21]$$

$$A^2B=[1/-5/21]$$

U=[0,0,1/0,1,-5/1,-5,21]

La determinante de u

u=-1

es controlable.

### *Paso 2: Polinomio Característico en Lazo Abierto*

El polinomio característico del sistema es:
$$\[
P(z) =|zI - A|
\]$$

P=[z,-1,0/0,z,-1/3,4,z+5]

$$PD=Z^{3}+5Z^{2}+4Z+3$$




### *Paso 3: Determinar la Matriz  T*

Los coeficientes del polinomio en lazo abierto son $$\( a_1 = 5 \)$$, $$\( a_2 = 4 \)$$, y $$\( a_3 = 3 \)$$. La matriz $$\( T \)$$ es simplemente la matriz identidad en este caso, ya que el sistema está en forma controlable.


T = I = 

### *Paso 4: Determinar el Polinomio Deseado*


$$\[
P_d(z) = (z + 1)(z + 2)(z + 3 - j2)(z + 3 + j2)
\]$$



$$\[
P_d(z) = z^4 + 9z^3 + 30z^2 + 42z + 20
\]$$


### *Paso 5: Calcular las Ganancias de Retroalimentación de Estados  K*



k=[8,25,38,17]




📚Ejercicio 2:


Consideremos un sistema con las siguientes matrices \( A \) y \( B \):

A=[0,1,0/0,0,1/-6,-11,-6]

B=[0/0/1]

tenemos los polos:

z = -1 + j

 z = -1 - j
 
 z = -5

### *Paso 1: Comprobación de Controlabilidad*

U=[0,0,1/0,1,-6/1,-6,25]=-1


es controlable

### *Paso 2: Polinomio Característico en Lazo Abierto*

El polinomio característico del sistema es:
$$\[
P = z^3 + 6z^2 + 11z + 6
\]$$

### *Paso 3: Determinar la Matriz \( T \)*

T = I 

### *Paso 4: Determinar el Polinomio Deseado*

Los polos deseados son \( z = -1 \pm j2 \) y \( z = -5 \). El polinomio deseado es:

$$\[
P_d(z) = (z + 1 - j2)(z + 1 + j2)(z + 5)
\]$$

$$\[
P_d(z) = z^3 + 7z^2 + 12z + 10
\]$$

### *Paso 5: Calcular las Ganancias de Retroalimentación de Estados \( K \)*


k=[4,1,1]


# concluciones

Conclusión Final
Los ejercicios muestran cómo, utilizando la controlabilidad y el diseño del controlador por retroalimentación de estados, es posible modificar el comportamiento de un sistema dinámico, moviendo los polos del sistema cerrado a las ubicaciones deseadas. Esto permite que el sistema tenga la respuesta deseada en términos de estabilidad y tiempo de respuesta, lo cual es crucial en la práctica de sistemas de control.

La metodología que hemos seguido, que incluye la comprobación de controlabilidad, el cálculo del polinomio característico, y la determinación de las ganancias de retroalimentación, es una forma sistemática y eficiente de diseñar controladores para sistemas dinámicos.
