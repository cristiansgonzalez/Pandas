# Pandas

'''
Carga de datos
'''
import pandas as pd
btc = pd.read_csv("btc.csv", index_col = "Nombre columna")

'''
Descripcion de los datos que tenemos almacenados
'''
btc.head() # Muestas las 5 primeras filas
btc.tail() # Muestra las ultimas 5 filas
btc.describe()
print(btc.dtypes)
print(btc.shape)
btc.columns.values

'''
Limpieza de los datos
 se pueden borrar o remplazar por otros datos
'''
filtrado = btc.dropna() # Elimina toda la fila que tenda Nan
filtrado = btc.fillna(argumento) # remplaza los Nan por el agurmento de entrada
filtrado = btc.fillna({'columna1': 0, 'columna2': "hola"}) # remplaza los Nan por el agurmento de entrada

'''
Filtro por columnas
'''
btc["Máximo"] # mostrar por columna
btc[["Máximo", "Vol."]] # mostrar un listado de columnas

'''
Filtrado por filas
'''
btc.iloc[0] # Realiza una busqueda por filas
btc.iloc[0:5] # Realiza una busqueda por rangos de filas
btc.iloc[[0, 3, 5]] # Realiza una busqueda por un listado de filas en especifico

'''
Filtrado por filas y columnas
'''
btc.loc[0] # Realiza una busqueda por el identificador de la fila
# Con el loc puedo  hacer filtrado por filas y columnas
btc.loc[[0, 3, 4], ["Open"]]

'''
Filtrado por condiciones
'''
btc[(btc["High"] > 2000) & (btc["Low"] > 2000)]

'''
Filtado por condiciones de texto
'''
btc[btc["Movimiento"].str.contains("Down")]

'''
Agregar columnas
'''
# se define una funcion

btc["nombre columna"] = df["columna que voy a enviar"].apply(nombre_funcion) #para enviar un solo argumento
btc["nombre columna"] = df.apply(nombre_funcion, axis = 1)

def movimiento(datos_filas):
    resultado = datos_filas["Open"] - datos_filas["Close"]
    #print(type(resultado))
    return resultado

def conversion(dato_columna):
    diferencia_pesos = dato_columna * 5000
    return diferencia_pesos

def Down_Up(datos):
    salida = []
    resta = pd.DataFrame({"resta": (datos["Open"] - datos["Close"])})

    for x in range(0, len(resta["resta"])):
        if(resta["resta"][x] < 0):
            salida.append("Down")
        elif(resta["resta"][x] > 0):
            salida.append("Up")
        else:
            salida.append("Equal")
    texto = pd.DataFrame({"Movimiento": salida})

    return texto.values
    
btc["Diferencia"] = btc.apply(movimiento, axis = 1)

btc["Diferencia pesos"] = btc["Diferencia"].apply(conversion)

btc["Movimiento"] = Down_Up(btc)

'''
Realizar operaciones por grupos de valores
'''
btc.groupby("Movimiento").mean()

btc.groupby("Movimiento").agg({
    "Diferencia": "max",
    "Open": "mean",
    "Low": "min"
})

'''
Graficos
'''
import matplotlib.pyplot as plt

resumen["Movimiento"].plot(kind = "bar")
plt.show()

btc.plot(kind = "scatter", x="Date", y="Open")
plt.show()

btc.plot(kind = "scatter", x="Date", y="Diferencia")
plt.show()

'''
Guardar el excel
'''
resumen.to_csv("resumen.csv")
ruta content
