
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


- La frecuencia <img src="/tex/190083ef7a1625fbc75f243cffb9c96d.svg?invert_in_darkmode&sanitize=true" align=middle width=9.81741584999999pt height=22.831056599999986pt/> y la duración <img src="/tex/2103f85b8b1477f430fc407cad462224.svg?invert_in_darkmode&sanitize=true" align=middle width=8.55596444999999pt height=22.831056599999986pt/> promedio de las ráfagas de actividad de un usuario a lo largo de un espacio
de tiempo <img src="/tex/4f4f4e395762a3af4575de74c019ebb5.svg?invert_in_darkmode&sanitize=true" align=middle width=5.936097749999991pt height=20.221802699999984pt/> nos dice que la probabilidad de transmitir es <img src="/tex/102385201bf065a922b14dca0418eb9a.svg?invert_in_darkmode&sanitize=true" align=middle width=61.54396379999998pt height=30.648287999999997pt/>. 
- Llamemos <img src="/tex/c9f058676b2164ecfaa2371164ec2323.svg?invert_in_darkmode&sanitize=true" align=middle width=21.23514854999999pt height=22.465723500000017pt/> al usuario que transmite en un momento dado. Llamemos <img src="/tex/7880f301aab6e338254f3b66a91a0c6d.svg?invert_in_darkmode&sanitize=true" align=middle width=286.97431290000003pt height=24.65753399999998pt/>. Ésta es la 
probabilidad de éxito en un ensayo de Bernoulli de probabilidad <img src="/tex/df5a289587a2f0247a5b97c1e8ac58ca.svg?invert_in_darkmode&sanitize=true" align=middle width=12.83677559999999pt height=22.465723500000017pt/>.
- La probabilidad de que cualquier <img src="/tex/8ea38e2adf995ba3a8661a5d13c17526.svg?invert_in_darkmode&sanitize=true" align=middle width=15.874636799999989pt height=22.465723500000017pt/> no transmita en el mismo instante es <img src="/tex/4377505b87e846b4ba0d83ead3a52dbb.svg?invert_in_darkmode&sanitize=true" align=middle width=102.6095433pt height=27.725679300000007pt/>.  
- El evento "está transmitiendo <img src="/tex/640168e471c7afd3936ed1814b93f944.svg?invert_in_darkmode&sanitize=true" align=middle width=17.77628489999999pt height=22.465723500000017pt/> y los demás no" es la conjunción de los eventos <img src="/tex/eed01977bd641ab1821110c0f8472bce.svg?invert_in_darkmode&sanitize=true" align=middle width=94.99531799999998pt height=27.725679300000007pt/>, 
que son independientes, y por lo tanto su probabilidad es el producto de las <img src="/tex/ef0de0b48cb187b636ae34b0aea8c1db.svg?invert_in_darkmode&sanitize=true" align=middle width=15.20454704999999pt height=22.465723500000017pt/>. 
- El evento "está transmitiendo un usuario cualquiera de entre los <img src="/tex/f9c4988898e7f532b9f826a75014ed3c.svg?invert_in_darkmode&sanitize=true" align=middle width=14.99998994999999pt height=22.465723500000017pt/>, y los demás no" equivale al evento 
compuesto "transmite <img src="/tex/640168e471c7afd3936ed1814b93f944.svg?invert_in_darkmode&sanitize=true" align=middle width=17.77628489999999pt height=22.465723500000017pt/> y los demás no, o transmite <img src="/tex/41c93ab7eaf30f73f32d515ad3fcc5f6.svg?invert_in_darkmode&sanitize=true" align=middle width=17.77628489999999pt height=22.465723500000017pt/> y los demás no, o transmite <img src="/tex/af9019f066d0c0eab52e85cf40381a6b.svg?invert_in_darkmode&sanitize=true" align=middle width=17.77628489999999pt height=22.465723500000017pt/> y los demás no...".
Como esos eventos elementales son disjuntos, su probabilidad es la suma de las probabilidades individuales.
- P(esté transmitiendo un usuario cualquiera de entre los <img src="/tex/f9c4988898e7f532b9f826a75014ed3c.svg?invert_in_darkmode&sanitize=true" align=middle width=14.99998994999999pt height=22.465723500000017pt/>, y los demás no):

<img src="/tex/dea825c5015046f884286843451e3cfa.svg?invert_in_darkmode&sanitize=true" align=middle width=666.5755107pt height=27.725679300000007pt/>.

- En el caso anterior, existen exactamente <img src="/tex/f9c4988898e7f532b9f826a75014ed3c.svg?invert_in_darkmode&sanitize=true" align=middle width=14.99998994999999pt height=22.465723500000017pt/> maneras de elegir el usuario que esté transmitiendo, 
lo que se refleja en el coeficiente <img src="/tex/f9c4988898e7f532b9f826a75014ed3c.svg?invert_in_darkmode&sanitize=true" align=middle width=14.99998994999999pt height=22.465723500000017pt/> de las probabilidades. Para analizar el caso donde transmiten <img src="/tex/103b826757951fc3932be9bf36ebca34.svg?invert_in_darkmode&sanitize=true" align=middle width=45.99298274999999pt height=22.831056599999986pt/> usuarios <img src="/tex/8ea38e2adf995ba3a8661a5d13c17526.svg?invert_in_darkmode&sanitize=true" align=middle width=15.874636799999989pt height=22.465723500000017pt/>,
hay muchas maneras de enumerar o elegir esos <img src="/tex/63bb9849783d01d91403bc9a5fea12a2.svg?invert_in_darkmode&sanitize=true" align=middle width=9.075367949999992pt height=22.831056599999986pt/> usuarios, 
y el factor que afecta a las probabilidades se expresa en forma de número combinatorio <img src="/tex/1a83719198e6a9265e8a51672a3dbfb0.svg?invert_in_darkmode&sanitize=true" align=middle width=26.71471109999999pt height=30.314440200000025pt/>:
- Hay <img src="/tex/156410ecc8fc743ca37e28a382050d1d.svg?invert_in_darkmode&sanitize=true" align=middle width=19.566193349999992pt height=22.831056599999986pt/> permutaciones o maneras de numerar los N usuarios. 
- De éstas, hay <img src="/tex/abdd0ce30ad6a7ae50f468899353b572.svg?invert_in_darkmode&sanitize=true" align=middle width=13.64158619999999pt height=22.831056599999986pt/> maneras, redundantes, de numerar o elegir los <img src="/tex/63bb9849783d01d91403bc9a5fea12a2.svg?invert_in_darkmode&sanitize=true" align=middle width=9.075367949999992pt height=22.831056599999986pt/> usuarios que transmiten.
- Por cada una de éstas, existen <img src="/tex/909007d6c99cc418909086ff5ddc3ac2.svg?invert_in_darkmode&sanitize=true" align=middle width=61.51817924999999pt height=24.65753399999998pt/> maneras, redundantes, de numerar los restantes. 
- La cantidad de combinaciones es <img src="/tex/d66ef0611aa8f08d1660dd6dde1a6d12.svg?invert_in_darkmode&sanitize=true" align=middle width=176.23492589999998pt height=30.314440200000025pt/>. Luego <img src="/tex/17b8dc37848c37991543a69c4d9752b7.svg?invert_in_darkmode&sanitize=true" align=middle width=420.02649644999997pt height=30.314440200000025pt/>.
- <img src="/tex/42074996a1179fc8035a4fc1b29c4509.svg?invert_in_darkmode&sanitize=true" align=middle width=468.92586839999996pt height=24.65753399999998pt/> donde <img src="/tex/b8bc815b5e9d5177af01fd4d3d3c2f10.svg?invert_in_darkmode&sanitize=true" align=middle width=12.85392569999999pt height=22.465723500000017pt/> es la función de distribución 
o función de probabilidad acumulada usando el cómputo anterior de exactamente <img src="/tex/63bb9849783d01d91403bc9a5fea12a2.svg?invert_in_darkmode&sanitize=true" align=middle width=9.075367949999992pt height=22.831056599999986pt/> usuarios.

## Ejemplo
Supongamos un universo de 50 usuarios donde cada uno está 10% del tiempo usando la aplicación. Investiguemos qué pasará 
con una cota de 10 usuarios.
- U1 transmite 10% del tiempo implica p(U1 esté transmitiendo) = p(U1) = P = 0.1. 
- Probabilidad de que cualquier Ui no transmita en el mismo instante es p(~Ui) = 1-P = 0.9.
- P(U1 ^ ~U2 ^ ~U3 ^ ...) = P * (1-P) * (1-P) * ... = P * (1-P)^(N-1) = 0.1 * 0.9^49 = .00057264
- P(esté transmitiendo un usuario cualquiera y los demás no) = P(U1 ^ ~U2 ^ ~U3 ^ ...)  +  P(~U1 ^ U2 ^ ~U3 ^ ...)  
+  P(~U1 ^ ~U2 ^ U3 ^ ...)  +... = N * P * (1-P) ^ (N-1) = 50 * 0.1 * 0.9 ^ 49 =  .02863205
- P(10 Ui transmitan y el resto no) = (N k) * p^k * (1-p)^(N-k) = C(50 10) * 0.1^10 * 0.9^49 =  
10272278170 * .000000000000572 = .005875743113240
- P(más de 10 usuarios) = 1 - P(10 o menos usuarios) = 1 - F(10). F(10) =  .99064539, 
luego P(más de 10 usuarios) = .00935460

Preparemos una tabla para esta aplicación hipotética donde hay 50 usuarios, con las probabilidades 
de "no más de k sesiones simultáneas" y la probabilidad de lo contrario ("más de k 
sesiones simultáneas"), para varios valores de k. Esto nos permitirá analizar los puntos de corte para determinar
las modalidades de licencia convenientes.

     k  P(no más de k)  P(más de k) 
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
     10	 .990645398375	.009354601625
     11	 .996780078826	.003219921174
     12	.998995380100	.001004619900
    13	.998995380100	.001004619900
    14	.998995380100	.001004619900

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
    
