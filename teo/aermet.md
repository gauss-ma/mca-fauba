---
nav_order: 6
published: false
---

# AERMET 

Fundamentos del preprocesador meteorológico AERMET.
{: .fs-6 .fw-300 }

<!-- center><iframe max-width="400" aspect-ratio="0.5625" src="https://www.youtube.com/embed/MUQfKFzIOeU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen>
</iframe></center -->


## Resumen

El objetivo de *AERMET* es el de usar mediciones meteorologicas representativas del dominio y computar algunos parámetros de la capa límite que permiten a AERMOD estimar perfiles de vientos, turbulencia y temperatura.

El crecimiento y estructura de la CLP está regulada por los flujos de calor y momentum que a su vez dependen de efectos de la superficie. El espesor de esta capa está incluenciada a escala local por características de la superficie: rugosidad (**z0**), albedo (**a0**), y disponibilidad de humedad (**b0**).

Los parámetros calculados por AERMET son:
+ Longitud de Monin-Obukhov (**L**)
+ Velocidad de fricción (** u* **)
+ Longitud de rugosidad (**z0**)
+ Flujo de Calor (**H**)
+ Escala de velocidad convectiva (** w* **)

Además AERMET provee estimaciones de alturas de mezcla mecánica (**z<sub>im</sub>**) y convectiva (**z<sub>ic</sub>**). Y define la estabilidad de la CLP por el signo de **H** (convectiva si H>0 y estable si H<0).

### Estimación para atmosfera convectiva

#### Balance de energía:

<center>
 R<sub>n</sub>= H + &lambda; E + G
</center>

Usando una estimación de G y considerando que B0=H/&lambda;E, podemos estimar H:

$$
H=\dfrac{0.9 R_n}{1+B_0^{-1})}
$$

Nos queda como incognita la radiación neta R<sub>n</sub> que puede ser observada o estimada.

$$
R_n= (-1 r(\phi))R-I_n
$$

En el caso de que haya nubosidad R se calcula como:

$$R=R_0(1 + b_1n^{b_2} $$

con coeficientes empiricos (Holstag, van Ulden, 1983) de b<sub>1</sub>=-0.75, y b<sub>2</sub>=3.4.

La radiación incidente para cielos claros (R0) está dado por:

$$ R_0 = a_1 \sin \phi + a_2 $$

Podemos llegar a:

$$ R_n = \dfrac{(1- r_{(\phi)}) R + c_1 T^6_{\text{ref}} - \sigma_{SB}T^4_{\text{ref}} - c^2\,n }{1 + c_3} $$



#### Velocidad de fricción y Longitud de Monin-Obukhov

Una vez que se estima el flujo de calor (H), AERMET estima la $u^*$, $L$ mediante un método iterativo, usando las siguentes expresiones:


$$
u_* = \dfrac{\kappa \,u}{  \ln(z_{\text{ref}}/z0) - \Psi_m(z_{\text{ref}}/L) + \Psi_m(z_{\text{0}}/L)  }
$$

y 

$$ L =-\dfrac{\rho c_p T u_*^3}{\kappa g H} $$



$$ \Psi_m (z_0/L) = 2\ln(\dfrac{1+\mu_0}{2})+\ln(\dfrac{1+\mu_0^2}{2}) - 2\tan^{-1}(\mu_0) + 0.5\,\phi $$


$$ \Psi_m (z_0/L) = 2\ln(\dfrac{1+\mu_0}{2})+\ln(\dfrac{1+\mu_0^2}{2}) - 2\tan^{-1}(\mu_0) + 0.5\,\phi $$


donde 
<center>
&mu;<sub></sub> = (1 -16 z<sub>ref</sub> / L )<sup>1/4</sup>

&mu;<sub>0</sub> = (1 -16 z<sub>0</sub> / L )<sup>1/4</sup>
</center>

El proceso requere un $u_*$ inicial, que se calcula contemplando los $\Psi$ igual a cero, y luego la iteración continua hasta que los valores de L difieren en menos del 1%.



#### Alturas de mezcla:


$$
z_{ic} \theta(z_{ic}) - \int_0^{z_{ic}} \theta(z) \,dz = (1 + 2A) \int_0^t \dfrac{H(t')}{\rho c_p} dt
$$

donde &theta;<sub>0</sub>(z) es la distribución vertical de la temperatura potencial dado por el sondeo de la mañana y el término derecho representa el flujo de calor acumulado en z=0. A=0.2

Una vez que conocemos z<sub>ic</sub> podemos obtener $w_*$ como:

$$
w_* = (\dfrac{gHz_{ic}}{\rho c_p T})^{1/3}
$$


### Estimación para atmosfera estable
Para el caso de atmosferas estables los calculos son más simples y no requieren procesos iterativos



Usando
<center>
H=-D c<sub>p</sub> u<sub>*</sub> &theta;<sub>*</sub>
</center>

Luego:

$$ \kappa \dfrac{u}{u_*} = \ln( \dfrac{z_{\text{ref}}}{z0} ) + \beta_m \dfrac{z_{\text{ref}}}{L}  $$


La velocidad de fricción se calcula como:

$$ u_* = C_D u/2 (1 + \sqrt{1- (2u_0/\sqrt{C_D} u)^2} ) $$

donde 

$$ C_D \dfrac{\kappa}{\ln{z_{\text{ref}}/z_0}} $$

y 

$$ u_0 = \sqrt{\beta_m z_{\text{ref}} g \theta_* / T} $$


$$ \theta_* = 0.09 (1-0.5n^2) $$

donde $n$ es la fracción opaca por cobertura nubosa.

El flujo de calor se computa como :

$$H=-\rho c_p u_* \theta_* $$

con $ u_* = \hat{u}_* u / \hat{u}_* $ y $ \theta_* =\hat{theta}_* u / \hat{theta}_*$

y 

$$ z_{im} = 2300 u_*^{3/2} $$





## Ejercicios:



## Bibliografía:
- "AERMOD Model Formulation and Evaluation", U.S.EPA. EPA-454/ R-18-003. April, 2018.

