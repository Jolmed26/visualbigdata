# Resultados de Tesis Challenge 🔍

Este proyecto se realiza luego de haber limpiado y preparado los datos para analisis, el resultado de dicho análisis previo se expone a continuación como contexto de una problemática que se busca solucionar y que tiene su origen en un análisis previamente realizado.

El análisis EDA permitió detectar errores a corregirse en cada una de sus etapas. Iniciando con la descripción de los datos, se detectó que los índices eran correctos y las variables parecían ser las adecuadas. En total, se contaba con 16 variables y 502 registros, de los cuales no todas tenían el formato correcto. Por tal motivo, las fechas se formatearon siguiendo el formato sugerido por la ISO 8601: año, mes y día. También se convirtieron las columnas de texto a formato string y se rellenaron los campos vacíos con valores NaN. Este proceso parece más adecuado para la etapa de limpieza de datos, pero en este caso fue necesario realizarlo en este punto para obtener la información general de la base de datos.

En total, se contaban con 6 variables cuantitativas y 10 categóricas.

Al revisar las variables con fechas (fecha de ingreso, fecha de baja y fecha de nacimiento), se detectó que había fechas de nacimiento correspondientes al año 2022, lo cual es erróneo, ya que la edad mínima permitida para trabajar es de 18 años. Por tal motivo, se sustituyeron las fechas de aquellas personas que no tenían los 18 años cumplidos por el mínimo legal de 18 años. Por otro lado, los valores nulos en las fechas se rellenaron con la media.

La variable objetivo cuenta con dos valores: baja y activo, y no tiene valores nulos. Sin embargo, los días laborados sí tenían valores nulos, lo cual es coherente ya que se detectó que esta variable era el resultado de restar la fecha de ingreso de la fecha de salida. Por ende, los empleados aún activos, al no tener una fecha de salida, no tenían un número de días laborados. No obstante, se determinó que la fecha de salida podía actualizarse a la fecha del último registro, y en los valores nulos se colocó la fecha de corte de los datos (30 de abril de 2024), restándola posteriormente de la fecha de ingreso, eliminando así los valores nulos de las variables inicialmente nombradas fecha de salida y días laborados.

En la variable "Crédito Infonavit" se detectaron valores inconsistentes como 'Si', 'NO', 'NO ' y 'SI', los cuales se deben unificar en dos categorías. También se identificaron 6 puestos distintos, de los cuales 1 corresponde a intendencia. Para este análisis, que se enfoca en empleados de producción, intendencia no entra en la categoría, por lo que se decidió eliminar esos registros.

En la variable "municipio" se detectó la presencia de "Jalisco", que no es un municipio; sin embargo, se asumió que se trataba de Zapopan.

Los salarios, tanto diario como mensual, también presentaban valores nulos y algunos se encontraban por debajo del salario mínimo vigente en la fecha de contratación. Estos valores se rellenaron con la media.

Estos cambios son algunos de los más relevantes en cuanto a la limpieza de datos y dieron como resultado visualizaciones que aportan gran valor al análisis posterior.

Primero, se detectó que la mayor cantidad de ingresos ocurrió en enero de 2022, lo cual coincide con el regreso a la "nueva normalidad" tras la pandemia de COVID-19.

La mayoría de los registros corresponden a empleados que ya han abandonado la empresa, con un total de 425 registros, mientras que 70 empleados siguen activos.

Los empleados trabajan en promedio 229 días en la empresa, pero la mayoría trabaja menos de 100 días. Además, en promedio, los empleados nacieron en 1991 y la mayoría son menores de 35 años y operadores de producción.

La información más relevante de este análisis exploratorio radica en que los empleados que llevan más tiempo en sus puestos son los auxiliares de almacén, mientras que los operadores de producción tienen el menor tiempo. No hay una diferencia significativa entre los distintos turnos, aunque los empleados que rotan turnos son los que tienen mayor rotación. En cuanto a la formación académica, los empleados con menor rotación son aquellos que están cursando la secundaria o que han concluido la preparatoria, mientras que los de mayor rotación son aquellos que tienen la secundaria incompleta o que están cursando la preparatoria.

Finalmente, se realizó un mapa de calor para analizar si existía alguna correlación entre el sueldo y los días laborados, obteniendo un resultado de -0.016. Esto indica que no se puede confirmar que exista una correlación significativa entre estas variables numéricas.

En conclusión, este primer análisis sienta las bases para análisis posteriores que buscarán predecir la rotación de personal, tomando como referencia las variables discutidas en este apartado.
