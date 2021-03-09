# Proyecto_DS_Equipo6
## Integrantes Equipo 6
- Flores Nogueira Diego David
- González Toledo Atzimba Alejandra
- Mendoza Martínez Arturo
- Tafolla Rosales Cristian

## Introducción
Muchas veces hemos querido explorar y resolver problemas a grandes escalas. De hecho, en nuestro proyecto anterior llegamos a ahondar en el PIB de nuestra nación. Con el fin de aplicar los conocimientos obtenidos a lo largo de este módulo, exploramos la idea de tomar un problema real en nuestro entorno escolar o de trabajo.
El dilema en el que quisimos poner nuestra atención y desmenuzar corresponde a los ingresos obtenidos por la Secretaría de Finanzas bajo concepto de tenencia vehicular.
> Cabe señalar que la data utilizada para este proyecto no es la original, sino está basada en datos reales.

## Identificación del problema
Año con año todos los titulares de un automóvil tienen que realizar el pago correspondiente al impuesto generado por poseer dicho vehículo. Tanto el Departamento de Finanzas como el de Movilidad de cada estado tienen como tarea verificar que se cumpla dicho trámite.
Como cada año, se es solicitado un resumen detallado con los siguientes puntos a destacar:
1. Suma monetaria acumulada después del pago de este impuesto por año.
2. Diferencia de ingresos obtenidos por cada periodo anual.
3. Inventario de vehículos con pagos registrados actualmente.
4. Tipo de placa de cada vehículo.

## Investigación
En esta ocasión, encontraremos que todos los vehículos registrados en este listado son automóviles, lo cual reduce a tres posibles tipos de placas:

| Tipo  | Definición | Ejemplo  |
| ------------- | ------------- | ------------- |
| Auto particular  | Corresponde a cualquier vehículo que actualmente se encuentre en circulación. | A00-AAA |
| Auto antiguo  | Vehículos con más de 30 años de antigüedad, los cuales realizaron la solicitud pertinente. | AA-000 |
| Autos que transportan personas con discapacidad  | Automóviles manejados por personas con algún impedimento físico. | 000-AA

Debemos tener en cuenta que en cada ocasión, dentro de lo posible, se genera una condonación parcial del pago correspondiente a la tenencia, esto cumpliendo con los requisitos que estipule el Departamento de Movilidad de la entidad federativa correspondiente.

## Soluciones anteriores

El Departamento de Finanzas generó el siguiente reporte preliminar:

| Año  | Acumulado |
| ------------- | ------------- |
| 0  | $22,225,856.00 |
| 2008  | $1,033,397.00 |
| 2009  | $1,647,045.00 |
| 2010  | $829,273.00 |
| 2011  | $2,001,800.00 |
| 2012  | $483,969.00 |
| 2013  | $33,005,528.00 |
| 2014  | $34,691,855.00 |
| 2015  | $33,513,172.00 |
| 2016  | $32,110,521.00 |
| 2017  | $35,740,995.00 |
| 2018  | $34,575,699.00 |
| 2019  | $33,777,617.00 |
| 2020  | $32,791,210.00 |

Esta tabla es el resultado obtenido de Excel, pero según los reportes estos resultados preliminares no son 100% confiables, puesto que se presentaron ciertos problemas con algunas fórmulas, como BUSCARV o EXTRAER, creemos que es mejor descartar el reporte como insumo y remitirnos al origen.

## En resumen

### Problema
Se quiere saber a cuánto ascienden los ingresos generados bajo el concepto de tenencia, así como las características relevantes de estos ingresos.

### Preguntas
1. ¿Cuánto dinero es acumulado después del pago de este impuesto por año?
2. ¿Cuál es la diferencia de ingresos obtenidos por cada periodo anual?
3. ¿Cuáles y cuántos vehículos están registrados actualmente?
4. ¿Cuál es el tipo de placa de cada vehículo?
5. ¿Esto cuadra con los informes entregados por el Departamento de Finanzas?

## Desarrollo
Recibimos un archivo con formato .csv, el cual contiene 27 columnas y 32,004 filas, el cuál tiene la siguiente estructura:

| Placa.año_fiscal  | Contiene, como su nombre lo dice, tanto la placa como el año fiscal en el que se hizo el pago. |
| ------------- | ------------- |
| monto pagado  | Cantidad en pesos correspondiente al pago de la tenencia. |
| concepto_lc.año_fiscal  | Contiene dos datos: concepto_lc, es el lugar donde fue efectuado el pago [37. Corresponsal, 38. Tesorerías disponibles, 39. En línea, 77. Transferencia electrónica], y año_fiscal, de igual forma, el año fiscal pero del siguiente pago.|

En las columnas posteriores se repiten alrededor de 12 veces más los nombres y contenidos de las columnas, y dentro de las mismas se encuentran los pagos realizados en diferentes años.

Este dataset fue generado desde el log de transacciones de la aplicación web, al cual solo tiene acceso el personal de la dependencia. Al solicitarlo, únicamente nos compartieron los datos disponibles en el archivo.
Consideramos que el tamaño de nuestro dataset nos brinda adecuada para responder nuestras preguntas iniciales y por las cuales decidimos realizar este proyecto.

### Algunos detalles

Durante la exploración de datos nos percatamos de que algunas columnas no venían con un nombre apropiado por lo cual se les asignó el nombre que consideramos adecuado y descriptivo siguiendo las buenas prácticas en python. Del mismo modo, ciertas columnas no venían con el tipo de dato que buscábamos para nuestro análisis por lo que fue necesario cambiarlo; estas columnas fueron monto_pagado y año_fiscal que pasaron de object a float e int, respectivamente

Otra cosa que encontramos durante la exploración fue la ausencia de algunos valores (datos con NaNs); debido a que si esos datos la información de esa fila está incompleta y no nos es útil, se removieron para tener un dataset limpio y homogéneo.

Requerimos de la creación de una nueva columna para facilitar el uso y lectura de la información. Para esto se analizaron las placas de los automóviles (con los criterios descritos anteriormente) para asignar el tipo de vehículo del que se trataba. A esta columna se le nombró como tipo.

Para tener una indexación pareja y sin saltos sus índices que pudieron suscitarse durante la limpieza de datos, se reindexó todo el dataset con el que trabajamos.

Decidimos guardar todos nuestros datos limpios y listos para utilizar en un .csv para facilitar su uso en el futuro.

## Resultados

Los resultados que obtuvimos del análisis no coinciden exactamente con los resultados preliminares del Departamento de Finanzas sin embargo tiene, relativamente hablando, una diferencia pequeña. Esta diferencia se le puede atribuir a los datos descartados durante su limpieza e incluso la diferencia podría ser resultado de los problemas que la dicha secretaría tuvo cuando los datos fueron analizados en Excel.

### Contestando a las preguntas

1. ¿Cuánto dinero es acumulado después del pago de este impuesto por año?

| Año Fiscal | Monto Pagado |
| ------------- | ------------- |
| 2008  | $1,020,682.00 |
| 2009  | $1,629,165.00 |
| 2010  | $803,832.00 |
| 2011  | $1,957,793.00 |
| 2012  | $457,897.00 |
| 2013  | $32,133,460.00 |
| 2014  | $33,544,159.00 |
| 2015  | $32,410,505.46 |
| 2016  | $31,165,153.00 |
| 2017  | $34,509,941.00 |
| 2018  | $33,638,920.11 |
| 2019  | $32,792,367.60 |
| 2020  | $31,791,033.00 |

2. ¿Cuál es la diferencia de ingresos obtenidos por cada periodo anual?

| Año Fiscal | Diferencia |
| ------------- | ------------- |
| 2009  | $608,483.00 |
| 2010  | -$825,333.00 |
| 2011  | $1,153,961.00 |
| 2012  | -$1,499,896.00 |
| 2013  | $31,675,563.00 |
| 2014  | $1,410,699.00 |
| 2015  | -$1,133,653.54 |
| 2016  | -$1,245,352.46 |
| 2017  | $3,344,788.00 |
| 2018  | -$871,020.89 |
| 2019  | -$846,552.51 |
| 2020  | -$1,001,334.60 |

3. ¿Cuál es el tipo de placa de cada vehículo?

| Tipo | Placa |
| ------------- | ------------- |
| Antiguo  | 18,352 |
| Discapacidad  | 35,091 |
| Particular  | 131,199 |

## Planes a futuro

Presentar la información de una forma más visual, como lo son los gráficos, nos parece importante y algo de los que nos gustaría realizar en un futuro. Además de la proyección de crecimiento o decrecimiento del capital obtenido por las instituciones estatales debido a el pago de la tenencia.

Una cosa que también sería interesante analizar y se podría hacer mediante los datos es el número de automóviles en circulación y cómo han aumentado o disminuido a lo largo de los años; junto con otros datos incluso se podría llegar a ver si los esfuerzos por la reducción del uso de automóviles está funcionando.

También, junto con otros datos, se puede inferir cómo es el transporte de las personas con discapacidad y si estas han tenido un aumento o una disminución de interés en la que se pueda profundizar en otro proyecto.


