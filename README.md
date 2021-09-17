# TALLER-PYTHON-ETSIDI
La motivación para realizar este proyecto surge de la necesidad en mi puesto de trabajo de verificar ciclos de curado de resina de 
reparaciones realizadas en piezas fabricadas en material compuesto. La verificación de los ciclos de curado consiste en validar las condiciones en las que las resinas aplicadasen las piezas cumplen con la normativa. Los datos consisten en valores de temperatura, dados por termopares situados en la pieza, frente al tiempo en que se han alcanzado estos valores de temperatura.
Dichos datos nos son entregados en un archivo .csv el cual con ayuda de una hoja Excel ordenamos los datos, graficamos y calculamos que los rangos de Temperatura/Tiempo están 
dentro de los valores permitidos por la normativa. 

En el programa que he realizado he hecho el cálculo de la rampa o pendiente de calentamiento, faltaría calcular la estabilización del ciclo de curado y la rampa de enfriamiento, además de superponer las gráficas de los termopares así como añadir una instrucción IF-ELSE que permitiera identificar los distintos tipos ciclos de curado y aplicar la normativa correspondiente a cada uno de ellos.

PROGRAMA


from datetime import datetime

import pandas as pd

ciclo_curado = pd.read_csv('ciclo curado2.csv', usecols= ['Time','TC 01','TC 02','TC 03','TC 04','TRATAMIENTO'])

ciclo_curado.plot.scatter(x='Time',y='TC 01')

ciclo_curado.plot.scatter(x='Time',y='TC 02')

ciclo_curado.plot.scatter(x='Time',y='TC 03')

ciclo_curado.plot.scatter(x='Time',y='TC 04')

tipo_de_ciclo = ciclo_curado['TRATAMIENTO'][1]

print(tipo_de_ciclo)

numerador_pendiente_calentamiento=ciclo_curado['TC 01'][25] - ciclo_curado['TC 01'][1]

format = '%H:%M:%S'

denominador_pendiente_calentamiento=datetime.strptime(ciclo_curado['Time'][25], format) - datetime.strptime(ciclo_curado['Time'][1], format)

unidades = "grados/min"

pendiente_calentamiento = numerador_pendiente_calentamiento/(denominador_pendiente_calentamiento.seconds/60)

if pendiente_calentamiento < 2.5:

    print(pendiente_calentamiento,unidades,"Está bien")
    
else:
    print(pendiente_calentamiento,unidades,"Está mal")
    
print(ciclo_curado)
