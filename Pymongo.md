# INSTRUCTIVO DE OPERACIONES PYMONGO

## Pasos previos

    Antes de empezer a trabajar con "Pymongo" debemos realizar las instalaciones previas.
    Una de las formas de instalar Pymongo puede ser con el siguiente comando:
**```**
        "pip install pymongo"
**```**
    Luego de tener instalado Pymongo pasaremos directamente al codigo, alli deberemos importar Pymongo y conectarlo con MongoDB
**```**
        import pymongo

        myclient = pymongo.MongoClient("URL de conexion del servidor mongo/")
**```**
    Ahora si, empezemos con lo que nos compete...

## Crear una base de datos

- Para crear una base de datos usaremos el siguiente comando:
**```**
    mydb = myclient["Nombre_de_la_base_de_datos"]
**```**
    Con este comando ya tendremos creado la base de datos con su respectivo nombre referente.

## Crear una coleccion

- La creacion de una coleccion es bastante facil, definiremos el nombre para llamar a esa coleccion y el nombre de la conexion como tal previa a un comando de pymongo el cual creara la coleccion "db[]":
**```**
    mycol = mydb["Nombre_Coleccion"]
**```**

## Insertar un Item 
- Para insertar un item se debe definir el item
documento = {"clave": "valor"}
resultado = coleccion.insert_one(documento)
print("ID del documento insertado:", resultado.inserted_id)
