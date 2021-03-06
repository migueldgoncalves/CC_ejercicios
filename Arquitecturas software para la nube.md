# Ejercicios del tema "Arquitecturas software para la nube"

## Ejercicio 1

**Buscar una aplicación de ejemplo, preferiblemente propia, y deducir qué patrón es el que usa. ¿Qué habría que hacer para evolucionar a un patrón tipo microservicios?**

R: La aplicación en análisis será la aplicación Renfe Horarios. Permite consultar horarios y precios de los trenes y avisos de ambito ferroviario mediante conexión a la Internet; e guardar localmente los trayectos favoritos. No cuenta con autenticación, formas de pago, o otras formas aparentes de integración con servicios de terceros dentro de la aplicación.
Siendo una aplicación de funcionalidad reducida, aunque destinada a pasageros de toda España, es posible que use la arquitectura en capas por su complejidad más reducida e mayor facilidad en corrigir errores.
Para evolucionar la aplicación a un patrón tipo microservicios, es necesário separar el acesso a los avisos y el acesso a los horarios en dos microservicios diferentes desacoplados, crear APIs para el acesso de la aplicación a los nuevos microservicios, así como separar la base de datos central en una para cada microservicio.

## Ejercicio 2

**En la aplicación que se ha usado como ejemplo en el ejercicio anterior, ¿podría usar diferentes lenguajes? ¿Qué almacenes de datos serían los más convenientes**

R: Asumiendo que se pretende evolucionar la aplicación a un patrón tipo microservicios, es totalmente posible que se utilicen diferentes lenguajes en la aplicación. Los tipos y parametros de los datos son fijos, dado que serán sólo horarios y precios de viajes, así como noticias con sus titulos, cuerpos e región. Siendo así, es viable utilizar bases de datos relacionales basadas en SQL e aprovechar su maturidad e compatibilidad entre plataformas.
