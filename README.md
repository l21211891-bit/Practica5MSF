[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=l21211891-bit/Practica5MSF)
# Práctica 5.5: Sistema musculoesquelético

## Información del estudiante
Africa Montserrat Rodriguez Garcia[l21211891]; L21211891@tectijuama.edu.mx
Modelado de Sistemas Fisiológicos

Ingeniería Biomédica

## Docente

Dr. Paul Antonio Valle Trujillo; paul.valle@tectijuana.edu.mx

Departamento de Ingeniería Eléctrica y Electrónica, Tecnológico Nacional de México/IT Tijuana, Blvd. Alberto Limón Padilla s/n, Tijuana, C.P. 22454, B.C., México.

## Descripción de la asignatura

El modelizado de sistemas fisiológicos es una herramienta importante en Ingeniería Biomédica, permite comprender el funcionamiento del cuerpo humano, así como diseñar y evaluar terapias y dispositivos médicos; se define como el proceso de formular modelos matemáticos o computacionales que representan el comportamiento y la interacción de los sistemas biológicos y fisiológicos. Esta asignatura pretende aportar al perfil del Ingeniero Biomédico la capacidad de realizar investigación científica en el área de Biología de Sistemas con la finalidad de dirigir y participar en equipos de trabajo interdisciplinarios en contextos nacionales e internacionales, así como de proporcionar soluciones informáticas para resolver problemas en el campo de la Ingeniería Biomédica con ética profesional; lo anterior al proporcionar al estudiante bases sólidas para modelizar sistemas y diseñar controladores para la solución de problemas en las áreas de atención médica y del sector industrial médico. La construcción de analogías entre circuitos eléctricos y sistemas fisiológicos para la formulación de modelos matemáticos y el diseño de controladores mediante la experimentación in silico brindan herramientas de gran aplicación en el quehacer profesional del Ingeniero Biomédico.

La asignatura de Modelado de Sistemas Fisiológicos forma parte del plan de estudios de la carrera en Ingeniería Biomédica con la siguiente competencia general del curso: Utiliza las propiedades de los circuitos RLC para describir la dinámica de sistemas fisiológicos, obtener modelos matemáticos y aplicar el control clásico, esto con el objetivo de integrar los principios de la Ingeniería de Control, la Electrónica Analógica y las Ciencias de la Computación con la Anatomía y Fisiología del cuerpo humano para proporcionar descripciones cuantitativas y cualitativas de sistemas fisiológicos complejos con el objetivo de modelizar, analizar, controlar, ilustrar y predecir su dinámica tanto en el corto como en el largo plazo.

## Objetivos

1. Convertir el diagrama mecánico al diagrama eléctrico.
2. Calcular la función de transferencia aplicando el principio de superposición.
3. Calcular el error en estado estacionario y la estabilidad en lazo abierto.
4. Emular y simular la respuesta del circuito en Simulink/Simscape a la señal impulso unitario.
5. Sintonizar las ganancias de un controlador PID para eliminar el error entre la entrada y la salida del sistema control-caso.
6. Obtener la respuesta en lazo abierto y en lazo cerrado con el controlador PID en Spyder/Python con la función de transferencia.

## Descripción detallada del sistema

El término F0 representa la fuerza desarrollada por el elemento contráctil activo del músculo, mientras que F(t) es la fuerza real que resulta después de tener en cuenta las propiedades mecánicas del músculo, y se asume que F0 = αF(t), donde 0 < α< 1; R representa la amortiguación viscosa inherente al tejido, mientras que Cp (elemento elástico paralelo) y Cs (elemento elástico en serie) reflejan las propiedades de almacenamiento elástico del sarcolema y los tendones musculares, respectivamente.

La configuración paralela se realiza para considerar las restricciones mecánicas impuestas a los componentes del modelo. Si el resorte Cp se estira en una longitud incremental x(t), toda la combinación en serie de R y Cs también se extenderá en la misma longitud. Además, la suma de la fuerza transmitida a través de las dos ramas de la configuración paralela debe ser igual a F(t). Aunque la suma de las extensiones de Cs y R tendrá que ser igual a x(t), las contribuciones individuales de longitud de Cs y R no necesitan ser iguales. Por lo tanto, si se asume que C\_{s} se estira una longitud x₁(t), entonces la extensión en la combinación paralela de R y F0 será x(t)-x₁(t). La velocidad con la que se extiende el amortiguador representado por R se obtiene al derivar x(t) - x1(t) con respecto al tiempo, es decir, d\[x(t) - x1(t)] /dt.

Palabras clave: Sistema musculoesqueletico; Circuito RC; Controlador PI; Modelo matematico; Simulaciones numericas 
## Modelo del sistema musculoesquelético

![Sistema musculoesquelético](Sistema%20Muscoloesquelitico.png)

*Figura 1. Modelo del sistema musculoesquelético en condición de control y con lesión de fibras musculares. Elaborado en BioRender.*

## Formulación matemática y análisis por superposición

Se aplica el principio de superposición para determinar la contribución de cada fuente. Se representa la fuerza de salida mediante **Fₛ(t)** y sus contribuciones mediante **Fₛ₁(t)** y **Fₛ₂(t)**.

### Circuito 1: apagando F₀(t)

Se considera únicamente la excitación F(t). Se parte de la suma de dos componentes de desplazamiento:

$$
x(t)=x_1(t)+x_2(t).
$$

Para las ramas equivalentes se escriben:

$$
x(t)=C_p\frac{dF_{s1}(t)}{dt},
$$

$$
x_1(t)=C_s\frac{d[F(t)-F_{s1}(t)]}{dt},
$$

$$
x_2(t)=\frac{F(t)-F_{s1}(t)}{R}.
$$

Sustituyendo en la ecuación inicial:

$$
C_p\frac{dF_{s1}(t)}{dt}
=C_s\frac{d[F(t)-F_{s1}(t)]}{dt}
+\frac{F(t)-F_{s1}(t)}{R}.
$$

Con condiciones iniciales nulas, la transformada de Laplace produce:

$$
C_p sF_{s1}(s)=C_s sF(s)-C_s sF_{s1}(s)
+\frac{F(s)-F_{s1}(s)}{R}.
$$

Agrupando los términos de salida:

$$
\left[(C_p+C_s)s+\frac{1}{R}\right]F_{s1}(s)
=\left(C_s s+\frac{1}{R}\right)F(s).
$$

Multiplicando por R y despejando:

$$
\frac{F_{s1}(s)}{F(s)}=
\frac{RC_s s+1}{R(C_p+C_s)s+1}.
$$

### Circuito 2: apagando F(t)

Se conserva la contribución de la fuente **F₀(t)=αF(t)**. El balance de la rama queda:

$$
-\alpha F(t)=R x(t)+\frac{1}{C_p+C_s}\int x(t)\,dt.
$$

Aplicando Laplace con condiciones iniciales nulas:

$$
-\alpha F(s)=R X(s)+\frac{X(s)}{(C_p+C_s)s}.
$$

De aquí:

$$
X(s)=-\alpha F(s)\frac{(C_p+C_s)s}{R(C_p+C_s)s+1}.
$$

La relación entre el desplazamiento y la fuerza de salida de la rama es:

$$
F_{s2}(s)=\frac{X(s)}{(C_p+C_s)s}.
$$

Por tanto:

$$
\frac{F_{s2}(s)}{F(s)}=
-\frac{\alpha}{R(C_p+C_s)s+1}.
$$

### Suma de las contribuciones

Por superposición:

$$
F_s(s)=F_{s1}(s)+F_{s2}(s).
$$

Sustituyendo ambas expresiones:

$$
F_s(s)=\left[\frac{RC_s s+1}{R(C_p+C_s)s+1}
-\frac{\alpha}{R(C_p+C_s)s+1}\right]F(s).
$$

La función de transferencia resultante es:

$$
H(s)=\frac{F_s(s)}{F(s)}=
\frac{RC_s s+1-\alpha}{R(C_p+C_s)s+1}.
$$

**Nota:** esta función relaciona la fuerza de salida con la fuerza de entrada. Si se selecciona el desplazamiento como salida, debe obtenerse por separado la relación G(s)=X(s)/F(s).

## Función de transferencia y alcance de la salida

La función obtenida mediante superposición es de **primer orden**:

$$
H(s)=\frac{RC_s s+1-\alpha}{R(C_p+C_s)s+1}.
$$

Sustituyendo los parámetros del instructivo en unidades eléctricas:

**Control sano (R = 100 Ω):**

$$
H_{control}(s)=\frac{0.001s+0.75}{0.011s+1}.
$$

**Caso de atrofia simulada (R = 10 000 Ω):**

$$
H_{caso}(s)=\frac{0.1s+0.75}{1.1s+1}.
$$

Las expresiones anteriores representan la transferencia de fuerza H(s). Para estudiar el desplazamiento debe establecerse la relación G(s)=X(s)/F(s) de acuerdo con la variable de salida seleccionada.

## Análisis de estabilidad

El polo de la función de transferencia desarrollada es:

$$
p=-\frac{1}{R(C_p+C_s)}.
$$

| Modelo | Denominador | Polo (s⁻¹) | Constante de tiempo |
|---|---|---:|---:|
| Control | 0.011s + 1 | −90.9091 | 0.011 s |
| Caso | 1.1s + 1 | −0.9091 | 1.1 s |

Ambos polos son reales y negativos: **ambas funciones son estables**. El polo del caso está más próximo al origen, por lo que su respuesta asociada a esta función de transferencia decae más lentamente. La constante de tiempo del caso es 100 veces la del control. Este resultado se deduce del modelo matemático y debe comprobarse con las simulaciones.

## Análisis de estado estacionario

Para una entrada escalón unitario y suponiendo estabilidad, el teorema del valor final proporciona:

$$
\lim_{t\to\infty}F_s(t)=\lim_{s\to0}H(s)=1-\alpha=0.75.
$$

En consecuencia, para **la salida de fuerza H(s)**, ambos modelos tienen la misma ganancia estática de 0.75. Si el error se define entre la entrada escalón unitario y esa salida, el error estacionario es **1 − 0.75 = 0.25**. En cambio, si se define como diferencia entre las salidas de control y caso ante el mismo escalón, el error estacionario entre ambas es **0**. Estos resultados no deben extrapolarse automáticamente a una salida de desplazamiento G(s) ni a la respuesta al impulso, que son análisis distintos.

## Diseño del controlador PID

El modelo del individuo sano se utiliza como referencia. Para la salida de desplazamiento indicada en el instructivo, el error es:

$$
e(t)=x_{control}(t)-x_{caso}(t).
$$

El controlador PID ideal puede expresarse como:

$$
u(t)=k_Pe(t)+k_I\int_0^t e(\tau)\,d\tau+k_D\frac{de(t)}{dt}.
$$

Se debe incorporar el bloque **PID Controller** en Simulink y utilizar **Tune** para determinar **kP**, **kI** y **kD**. El objetivo es una respuesta estable que reduzca la diferencia entre el caso simulado y el control sano. Después se comparan las tres respuestas: **control**, **caso sin controlador** y **caso con PID**.

| Parámetro | Valor obtenido |
|---|---|
| kP | Pendiente de sintonización |
| kI | Pendiente de sintonización |
| kD | Pendiente de sintonización |

No se asignan ganancias ficticias ni se afirma un desempeño que todavía no esté respaldado por resultados.

## Implementación en Python

Se deben implementar las funciones de transferencia del control y del caso con las mismas condiciones que MATLAB/Simulink, calcular la respuesta al impulso y reproducir el sistema con las ganancias PID obtenidas en **Tune**. El código puede ejecutarse en Visual Studio Code y debe guardar figuras para comparar lazo abierto y lazo cerrado. Las librerías dependen del archivo Python efectivamente utilizado; normalmente pueden emplearse NumPy, Matplotlib y `python-control`.

## Resultados y verificación cruzada

La verificación requiere comparar cinco implementaciones: ecuaciones en Simulink, función de transferencia en Simulink, circuito equivalente en Simscape, cuaderno MATLAB y script Python. Las respuestas deben compararse con parámetros, entrada, salida y condiciones iniciales iguales.

| Resultado | Estado |
|---|---|
| Parámetros control/caso | Identificados en el instructivo |
| Análisis por superposición | Desarrollado a partir de `analisis.pdf` |
| Funciones Hcontrol y Hcaso | Calculadas |
| Polos y estabilidad de H(s) | Calculados |
| Estado estacionario de H(s) | Calculado |
| Simulaciones en MATLAB/Simulink | Agregar resultados reales |
| Simscape Electrical | Agregar circuito y resultados |
| Ganancias PID | Agregar valores de Tune |
| Gráficas de Python | Agregar resultados reales |
| Comparación entre plataformas | Completar con evidencias |

## Conclusiones

El modelo musculoesquelético permite estudiar el efecto de la elasticidad y el amortiguamiento sobre una respuesta dinámica mediante una representación mecánica y su analogía eléctrica. El procedimiento por superposición desarrollado en el análisis conduce a una función de transferencia de primer orden para la fuerza equivalente, con polos negativos en las dos condiciones estudiadas. El aumento de R produce una respuesta temporal más lenta en ese modelo, sin modificar su ganancia estática. La implementación en Simulink, Simscape y Python permitirá comprobar estas predicciones y estudiar el efecto de un controlador PID; para establecer conclusiones experimentales o de simulación definitivas es necesario incorporar las gráficas y las ganancias obtenidas.


## Lista de archivos incluidos en el repositorio

1. Cuaderno computacional de MATLAB \[.mlx].
2. Modelo de Simulink \[.slx].
3. Archivos de Spyder \[.py].
4. Imagen con los parámetros del controlador.
5. Imágenes de las simulaciones \[.pdf y .png].
6. Evidencia del análisis matemático: función de transferencia, error en estado estacionario y estabilidad en lazo abierto.

## Referencias

\[1] P. A. Valle, Syllabus para Modelado de Sistemas Fisiológicos, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2025. Permalink: https://biomath.xyz/course/

\[2] M. C. Khoo, Physiological Control Systems Analysis Simulation, and Estimation, 2nd ed. Piscataway, New Jersey, USA: IEEE Press, 2018, Section 4, Page 93.

\[3] N. S. Nise, Control Systems Engineering, 8th ed. Hoboken, New Jersey, USA: John Wiley \& Sons, 2020.

