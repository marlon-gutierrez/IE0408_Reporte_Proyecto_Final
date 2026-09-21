# Controlador PID Analógico para un Filtro Sallen-Key

Diseño, modelado e implementación experimental de un **controlador PID analógico** para una planta correspondiente a un filtro Sallen-Key de segundo orden.

El proyecto fue desarrollado como parte del curso **IE0408 – Laboratorio de Electrónica II** de la **Universidad de Costa Rica (UCR)** e incluyó el proceso completo desde la caracterización de la planta hasta la implementación y validación experimental del sistema de control en hardware.

## Descripción

El objetivo principal del proyecto fue diseñar e implementar un controlador PID analógico capaz de controlar la respuesta de un filtro Sallen-Key de segundo orden.

El desarrollo incluyó:

* Implementación física de la planta Sallen-Key.
* Medición experimental de la respuesta al escalón.
* Identificación y modelado de la planta mediante MATLAB.
* Diseño y ajuste del controlador PID.
* Implementación analógica de las acciones proporcional, integral y derivativa.
* Integración del sistema completo en lazo cerrado.
* Pruebas experimentales mediante instrumentación de laboratorio.
* Evaluación del seguimiento de referencia y rechazo de perturbaciones.

## Arquitectura del sistema

El sistema de control implementado sigue la estructura:

**Referencia → Cálculo del error → Controlador PID → Planta Sallen-Key → Realimentación**

La señal de error se obtiene mediante la diferencia entre la referencia y la salida realimentada de la planta.

El controlador fue implementado utilizando una estructura PID en paralelo:

$$
C(s)=K_p+\frac{K_i}{s}+K_d s
$$

Las acciones proporcional, integral y derivativa fueron implementadas mediante circuitos con amplificadores operacionales y posteriormente combinadas mediante una etapa sumadora.

## Planta Sallen-Key

La planta utilizada corresponde a un **filtro pasa bajos Sallen-Key de segundo orden**, implementado físicamente mediante un amplificador operacional LF353 y componentes pasivos.

Para caracterizar su comportamiento, se aplicó una entrada escalón y se midieron simultáneamente las señales de entrada y salida utilizando un osciloscopio.

Los datos experimentales fueron posteriormente procesados en MATLAB y utilizados con **System Identification Toolbox** para obtener un modelo de segundo orden con tiempo muerto.

El modelo identificado presentó un ajuste del **98.3 %** respecto a la respuesta experimental:

$$
G(s)=
\frac{274.74}
{s^2+4.61s+118.86}
e^{-0.00015s}
$$

También se obtuvo un modelo analítico del circuito Sallen-Key para utilizarlo como referencia y comparar su comportamiento con el modelo identificado experimentalmente.

## Diseño del controlador PID

El modelo experimental de la planta fue utilizado en MATLAB para realizar el diseño del controlador.

Los parámetros obtenidos para el PID fueron:

| Parámetro |   Valor |
| --------- | ------: |
| \(K_p\)   |  4.8781 |
| \(K_i\)   | 21.7534 |
| \(K_d\)   |   0.273 |

A partir de estos valores se calcularon las constantes de tiempo de las acciones integral y derivativa:

$$
T_i=\frac{K_p}{K_i}=0.224\,s
$$

$$
T_d=\frac{K_d}{K_p}=0.056\,s
$$

Posteriormente, estos parámetros fueron convertidos en valores de resistencias y capacitores para realizar la implementación física del controlador.

## Implementación en hardware

El controlador PID fue implementado utilizando **amplificadores operacionales LF353** y redes resistivas y capacitivas.

El sistema analógico está compuesto por:

* Etapa restadora para obtener la señal de error.
* Etapa proporcional.
* Etapa integral.
* Etapa derivativa.
* Etapa sumadora.
* Planta Sallen-Key.
* Lazo de realimentación.

El circuito completo fue ensamblado y probado experimentalmente utilizando equipo de laboratorio.

## Validación experimental

Una vez implementado el sistema completo, se realizaron diferentes pruebas para analizar su comportamiento dinámico.

Se evaluaron tres condiciones principales:

1. Cambios manuales en la señal de referencia.
2. Referencia mediante una señal cuadrada.
3. Aplicación de una perturbación externa a la planta.

El sistema logró seguir los cambios en la referencia y recuperar el estado estacionario después de la aplicación de perturbaciones.

### Resultados experimentales

| Parámetro                             | Resultado |
| ------------------------------------- | --------: |
| Sobrepaso máximo \(M_p\)              |   10.25 % |
| Tiempo muerto \(L\)                   |    105 ms |
| Tiempo de asentamiento al 2 % \(t_s\) |    310 ms |

Los resultados experimentales presentan diferencias respecto al modelo matemático debido a efectos propios de la implementación física, como tolerancias de los componentes, características reales de los amplificadores operacionales, offsets y dinámicas adicionales del circuito.

## Herramientas y tecnologías

![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?style=for-the-badge)
![TINA-TI](https://img.shields.io/badge/TINA--TI-BB0000?style=for-the-badge)
![Electrónica Analógica](https://img.shields.io/badge/Electrónica%20Analógica-333333?style=for-the-badge)
![Control](https://img.shields.io/badge/Sistemas%20de%20Control-00599C?style=for-the-badge)

### Áreas aplicadas

* Electrónica analógica
* Amplificadores operacionales
* Control PID
* Identificación de sistemas
* Modelado de sistemas
* Simulación de circuitos
* Implementación de hardware
* Instrumentación electrónica
* Adquisición y análisis de datos
* Validación experimental

## Equipo utilizado

Durante las pruebas experimentales se utilizó instrumentación de laboratorio, incluyendo:

* Osciloscopio digital Rigol MSO5074
* Generador de señales Agilent
* Multímetro digital
* Fuentes de alimentación DC Rigol y Agilent

## Documentación

El reporte completo del proyecto, incluyendo desarrollo teórico, cálculos, diseño de circuitos, simulaciones, mediciones experimentales y discusión de resultados, se encuentra disponible en:

[`IE0408_Final_Report.pdf`](IE0408_Final_Report.pdf)

## Autores

**Marlon Gutiérrez Vásquez**
Ingeniería Eléctrica
Universidad de Costa Rica

**José David Monge Gutiérrez**
Ingeniería Eléctrica
Universidad de Costa Rica

Proyecto académico desarrollado para **IE0408 – Laboratorio de Electrónica II**, Universidad de Costa Rica.
