
# Distribución multinomial

En el libro de Redes de Kurose se trata estadísticamente el problema de averiguar cuántos de entre <img src="/tex/55a049b8f161ae7cfeb0197d75aff967.svg?invert_in_darkmode&sanitize=true" align=middle width=9.86687624999999pt height=14.15524440000002pt/> usuarios 
comparten efectivamente un enlace en un momento dado, conociendo la frecuencia y duración de las ráfagas de actividad de 
un usuario. 

El problema tiene otros análogos, como el de calcular la cantidad de licencias concurrentes adecuada para una 
aplicación de red.
En este caso se trataría de averiguar cuántos usuarios usarán concurrentemente un servidor, si es que la aplicación 
tiene noción de sesión. De lo contrario, habrá que calcular la duración promedio de una respuesta y asumirla
como la duración de una sesión virtual. 

Para aplicar el tratamiento de Kurose hay que conocer la frecuencia y duración de las ráfagas de actividad de un usuario, 
y con esos datos determinar la probabilidad de transmitir en un momento dado. 

El planteo es como sigue:


- La frecuencia f y la duración d promedio de las ráfagas de actividad de un usuario a lo largo de un espacio
de tiempo t nos dice que la probabilidad de transmitir es <img src="/tex/426a016d185b9625aee16e564d70a72b.svg?invert_in_darkmode&sanitize=true" align=middle width=82.80805335pt height=24.65753399999998pt/>. 
- Llamemos U1 al usuario que transmite en un momento dado. Llamemos <img src="/tex/f0cc4ba9e979b56a309c7d07acfb5c66.svg?invert_in_darkmode&sanitize=true" align=middle width=276.0154254pt height=24.65753399999998pt/>. Ésta es la 
probabilidad de éxito en un ensayo de Bernoulli de probabilidad <img src="/tex/df5a289587a2f0247a5b97c1e8ac58ca.svg?invert_in_darkmode&sanitize=true" align=middle width=12.83677559999999pt height=22.465723500000017pt/>.
- La probabilidad de que cualquier Ui no transmita en el mismo instante es <img src="/tex/be39e9c6368b0601cfd26678b9365bf0.svg?invert_in_darkmode&sanitize=true" align=middle width=108.27941519999999pt height=24.65753399999998pt/>.  
- El evento "está transmitiendo U1 y los demás no" es la conjunción de los eventos {U1, ~U2, ~U3, ...} 
que son independientes, y por lo tanto su P es el producto de las Pi. 
- El evento "está transmitiendo un usuario cualquiera de entre los N, y los demás no" equivale al evento 
compuesto "transmite U1 y los demás no, o transmite U2 y los demás no, o transmite U3 y los demás no...".
Como esos eventos elementales son disjuntos, su probabilidad es la suma de las probabilidades individuales.
- P(esté transmitiendo un usuario cualquiera de entre los N, y los demás no) =  P(U1 ^ ~U2 ^ ~U3 ^ ...)  
+  P(~U1 ^ U2 ^ ~U3 ^ ...)  +  P(~U1 ^ ~U2 ^ U3 ^ ...)  +... = N * p * (1-p) ^ (N-1)
- En el caso anterior, existen exactamente N maneras de elegir el usuario que esté transmitiendo, 
lo que se refleja en el coeficiente N de las probabilidades. Para analizar el caso donde transmiten <img src="/tex/103b826757951fc3932be9bf36ebca34.svg?invert_in_darkmode&sanitize=true" align=middle width=45.99298274999999pt height=22.831056599999986pt/> usuarios Ui,
hay muchas maneras de enumerar o elegir esos k usuarios, 
y el factor que afecta a las probabilidades se expresa en forma de número combinatorio. 
    - Hay $N!$ permutaciones o maneras de numerar los N usuarios. 
    - De éstas, hay $k!$ maneras, redundantes, de numerar o elegir los k usuarios que transmiten.
    - Po cada una de éstas, existen $(N - k)!$ maneras, redundantes, de numerar los restantes. 
    - La cantidad de combinaciones es $N! / [k! * (N - k)!] = (N k)$. Luego P(k Ui transmitan 
y el resto no) = <img src="/tex/6b2115bc86d2735014af6b7e3cdfaa7a.svg?invert_in_darkmode&sanitize=true" align=middle width=190.15377809999998pt height=29.190975000000005pt/>.


## Ejemplo
Supongamos que cada usuario está 10% del tiempo usando la aplicación. Investiguemos qué pasará con 10 usuarios.
- U1 transmite 10% del tiempo implica p(U1 esté transmitiendo) = p(U1) = P = 0.1. 
- Probabilidad de que cualquier Ui no transmita en el mismo instante es p(~Ui) = 1-P = 0.9.
- P(U1 ^ ~U2 ^ ~U3 ^ ...) = P * (1-P) * (1-P) * ... = P * (1-P)^(N-1) = 0.1 * 0.9^49 = .00057264
- P(esté transmitiendo un usuario cualquiera y los demás no) = P(U1 ^ ~U2 ^ ~U3 ^ ...)  +  P(~U1 ^ U2 ^ ~U3 ^ ...)  
+  P(~U1 ^ ~U2 ^ U3 ^ ...)  +... = N * P * (1-P) ^ (N-1) = 50 * 0.1 * 0.9 ^ 49 =  .02863205
- P(10 Ui transmitan y el resto no) = (Nps k) * p^k * (1-p)^(Nps-k) = (50 10) * 0.1 ^ 10 * 0.9 ^ 49 =  
10272278170 * .000000000000572 = .005875743113240
- P(más de 10 usuarios) = 1 - P(10 o menos usuarios) = 1 - F(10) donde F es la función de distribución 
o función de probabilidad acumulada usando el cómputo anterior de exactamente k usuarios. F(10) =  .99064539, 
luego P(más de 10 usuarios) = .00935460
- Ofrecer la licencia se parece a ofrecer la garantía de una batería, querés saber cuánto va a aguantar antes 
de romperse y entonces fijás la garantia en un picosegundo antes de que se rompa. Similarmente acá te interesa 
saber cuántos vas a tener laburando simultáneamente para que les quede chico el contrato lo antes posible y 
ofrecerles el segmento de licencia adecuado que vale cinco veces más que el anterior. Acá la tablita para 50 
usuarios, con las probabilidades de "no más de k sesiones simultáneas" y la prob de lo contrario ("más de k 
sesiones simultáneas"). Siempre suponiendo que c/u trabaja en promedio un 10% del tiempo. Como ves, más de 10 
chabones no hay casi nunca.


## Script
Se adjunta el script en bc (la calculadorita de Unix) para toquetear a piacere una vez que sepas la tasa de uso. Modificando el "scale" se obtiene más precisión, acá con scale=12 para 10 o 12 sesiones ya prácticamente no hay diferencia.
0	.005153775207	.994846224793
1	.033785859692	.966214140308
2	.111728756344	.888271243656
3	.250293905948	.749706094052
4	.431198406817	.568801593183
5	.616123007710	.383876992290
6	.770226841775	.229773158225
7	.877854916367	.122145083633
8	.942132794247	.057867205753
9	.975462064259	.024537935741
10	.990645398375	.009354601625
11	.996780078826	.003219921174
12	.998995380100	.001004619900
13	.998995380100	.001004619900
14	.998995380100	.001004619900

