
# Distribución multinomial

En el libro de Redes de Kurose se trata estadísticamente el problema de averiguar cuántos de entre $n$ usuarios 
comparten efectivamente un enlace en un momento dado, conociendo la frecuencia y duración de las ráfagas de actividad de 
un usuario. 

El problema tiene otros análogos, como el de calcular la cantidad de licencias concurrentes adecuada para una 
aplicación de red. En este caso se trataría de averiguar cuántos usuarios tendrán sesiones concurrentemente un servidor, si es que la aplicación tiene noción de sesión. De lo contrario, habrá que calcular la duración promedio de una respuesta y asumirla
como la duración de una sesión virtual. 

Para aplicar el tratamiento de Kurose hay que conocer la frecuencia y duración de las ráfagas de actividad de un usuario, 
y con esos datos determinar la probabilidad de transmitir en un momento dado. 

El planteo es como sigue:


- A lo largo de un espacio de tiempo $t$, la cantidad de veces $v$ que un usuario interactúa con el sistema nos da la frecuencia, $f = v / t$. Junto con la duración $d$ promedio de sus ráfagas de actividad, se puede calcular la probabilidad de que ese usuario esté transmitiendo en un momento dado como $P = f \times d$. 
- Llamemos $U1$ al usuario que transmite en un momento dado. Llamemos $p(U1\ esté\ transmitiendo) = p(U1) = P$. Ésta es la 
probabilidad de éxito en un ensayo de Bernoulli de probabilidad $P$.
- La probabilidad de que cualquier $U_i$ no transmita en el mismo instante es $p(\overline U_i) = 1-P$.  
- El evento "está transmitiendo $U_1$ y los demás no" es la conjunción de los eventos ${U_1, \overline U_2, \overline U_3, ...}$, 
que son independientes, y por lo tanto su probabilidad es el producto de las $P_i$. 
- El evento "está transmitiendo un usuario cualquiera de entre los $N$, y los demás no" equivale al evento 
compuesto "transmite $U_1$ y los demás no, o transmite $U_2$ y los demás no, o transmite $U_3$ y los demás no...".
Como esos eventos elementales son disjuntos, su probabilidad es la suma de las probabilidades individuales.
- P(esté transmitiendo un usuario cualquiera de entre los $N$, y los demás no):

$P(U_1 \cap \overline U_2 \cap \overline U_3 \cap \ldots)  +  
P(\overline U_1 \cap U_2 \cap \overline U_3 \cap \ldots)  +  
P(\overline U_1 \cap \overline U_2 \cap U_3 \cap \ldots)  + \ldots
= N \times P \times (1-P) ^ {N-1}$.

- En el caso anterior, existen exactamente $N$ maneras de elegir el usuario que esté transmitiendo, 
lo que se refleja en el coeficiente $N$ de las probabilidades. Para analizar el caso donde transmiten $k < N$ usuarios $U_i$,
hay muchas maneras de enumerar o elegir esos $k$ usuarios, 
y el factor que afecta a las probabilidades se expresa en forma de número combinatorio ${N \choose k}$:
- Hay $ N! $ permutaciones o maneras de numerar los N usuarios. 
- De éstas, hay $ k! $ maneras, redundantes, de numerar o elegir los $k$ usuarios que transmiten.
- Por cada una de éstas, existen $(N - k)!$ maneras, redundantes, de numerar los restantes. 
- La cantidad de combinaciones es $\frac{N!}{k!  (N - k)!} = {N \choose k}$. Luego $P(k\ U_i\ transmitan\ y\ el\ resto\ no) = {N \choose k} * P^k * (1-P)^{N-k}$.
- $P(más\ de\ k\ usuarios) = 1 - P(k\ o\ menos\ usuarios) = 1 - F(k)$ donde $F$ es la función de distribución 
o función de probabilidad acumulada usando el cómputo anterior de exactamente $k$ usuarios.

## Ejemplo
Supongamos un universo de 50 usuarios donde cada uno está 10% del tiempo usando la aplicación. Investiguemos qué pasará 
con una cota de 10 usuarios.
- U1 transmite 10% del tiempo implica p(U1 esté transmitiendo) = p(U1) = P = 0.1. 
- Probabilidad de que cualquier Ui no transmita en el mismo instante es p(~Ui) = 1-P = 0.9.
- P(U1 ^ ~U2 ^ ~U3 ^ ...) = P * (1-P) * (1-P) * ... = P * (1-P)^(N-1) = 0.1 * 0.9^49 = .00057264
- P(esté transmitiendo un usuario cualquiera y los demás no) = P(U1 ^ ~U2 ^ ~U3 ^ ...)  +  P(~U1 ^ U2 ^ ~U3 ^ ...)  
+  P(~U1 ^ ~U2 ^ U3 ^ ...)  +... = N * P * (1-P) ^ (N-1) = 50 * 0.1 * 0.9 ^ 49 =  .02863205
- P(10 Ui transmitan y el resto no) = (N k) * P^k * (1-P)^(N-k) = C(50 10) * 0.1^10 * 0.9^49 =  
10272278170 * .000000000000572 = .005875743113240
- P(más de 10 usuarios) = 1 - P(10 o menos usuarios) = 1 - F(10). F(10) =  .99064539, 
luego P(más de 10 usuarios) = .00935460

Preparemos una tabla para esta aplicación hipotética donde hay 50 usuarios, con las probabilidades 
de "no más de k sesiones simultáneas" y la probabilidad de lo contrario ("más de k 
sesiones simultáneas"), para varios valores de k. Esto nos permitirá analizar los puntos de corte para determinar
las modalidades de licencia convenientes.

     k    P(no más de k)   P(más de k) 
     0    .005153775207    .994846224793
     1    .033785859692    .966214140308
     2    .111728756344    .888271243656
     3    .250293905948    .749706094052
     4    .431198406817    .568801593183
     5    .616123007710    .383876992290
     6    .770226841775    .229773158225
     7    .877854916367    .122145083633
     8    .942132794247    .057867205753
     9    .975462064259    .024537935741
    10    .990645398375    .009354601625
    11    .996780078826    .003219921174
    12    .998995380100    .001004619900
    13    .998995380100    .001004619900
    14    .998995380100    .001004619900

## Script
Se adjunta el script en bc (la calculadora de Unix) que produce la tabla anterior. Modificando el "scale" se obtiene mayor precisión. Con scale=12, para 10 o 12 sesiones ya prácticamente no hay diferencia apreciable.

    #!/usr/bin/bc -q
    scale=12
    define fact(x)
    {
             if(x <= 1)
                     return 1;
             return x * fact(x-1);
    }
    #fact(3)
    #fact(5)
    #fact(13)
    define comb(n,k)
    {
             return fact(n) / (fact(k) * fact(n-k));
    }
    #comb(5,1)
    #comb(5,2)
    #comb(13,7)
    define fprob(n,k,p)
    {
             return comb(n,k) * (p ^ k) * ((1-p) ^ (n-k));
    }
    define fdistrib(n,k,p)
    {
            suma = 0;
             for(i=0; i<=k; i++) {
                     suma += fprob(n,i,p);
             }
             return suma;
    }
    
    print "k, prob de <= k usuarios, prob de > k usuarios trabajando a la vez\n"
    
    for(j=0; j<15; j++) {
           f = fdistrib(50,j,0.1)
           print j,"\t",f,"\t",1-f,"\n"
    }
    
    quit
    
