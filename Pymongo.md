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

        myclient = pymongo.MongoClient("URL de conexion del servidor mongo")

**```**
 Ahora si, empezemos con lo que nos compete...

## Crear una base de datos

- Para crear una base de datos usaremos el siguiente comando:

**```**
    mydb = myclient["Nombre_de_la_base_de_datos"]
**```**

    Con este comando ya tendremos creado la base de datos con su respectivo nombre referente.

## Crear una coleccion

- La creacion de una coleccion es bastante facil, definiremos el nombre para llamar a esa coleccion y el nombre de la conexion como tal previa a un comando de pymongo el cual creara la coleccion "db[  ]":

**```**
    mycol = mydb["Nombre_Coleccion"]
**```**

## Crear e insertar un Item

- Para insertar un item se debe definir el item para crearlo y crear otra definicion para insertar el item mediante los siguientes comandos:

**```**
    documento = {"clave" : "valor"}

    resultado = mycol.insert_one(documento)
**```**

## Eliminar un Item

- Para eliminar un item seguiremos los siguientes comandos, en este caso puede ser utilizado como un filtro de distintas expresiones:

**```**
   filtro = {"clave" : "valor"}

    resultado = mycol.delete_one(filtro)
**```**

De esta forma borraremos un item en forma de filtro(puede ser utilizado para muchas ocasiones distintas ademas de un filtro).

## Actualizar un Item

- Para actualizar un solo item deberemos seguir la siguiente logica:

**```**
item_A = {"clave" : "valor"}

item_B = {"$set" : {"clave" : "nuevo_valor"}}

actualizar_item = mycol.update_one(item_A,item_B)
**```**

    Dependiendo el caso, podemos reemplazar el comando $set por $inc:

        - $set  (Reemplaza el  valor del item por otro).

        - $inc  (Aumenta el valor del item junto a otro valor).

## Actualizar varios Items

- Para varios items podemos utilizar un update_many para actualizar varios valores:

**```**
item_A = {"clave" : "valor"}
item_B = {"$set" : {"clave": "nuevo_valor"}}
resultado = collection.update_many(item_A, item_B )
**```**

  Un ejemplo distinto para esto podria ser el $gte : "valor" que tomara los valores iguales o mayores a ese valor  (Podemos aplicar la misma mecanica de $set & $inc)

## Borrar muchos Items

- En este caso usaremos lo mismo, delete_many para varios items a eliminar: 

**```**
    mayores_a_17 = {edad:{$gte : 18 }} 
    Listado =   {id_: 1, nombre : "Juan", edad: 25}
                {id_: 2, nombre : "Pancho", edad: 40}
                {id_: 3, nombre : "Marcelito", edad: 17}
    resultado = collection.delete_many(mayores_a_17, Listado)
**```**

Aqui tambien podemos utilizar $gte : "valor" que tomara los valores iguales o mayores a ese valor y los eliminara. En el ejemplo se eliminara a los que son mayores de 17, en este caso, Pancho y Marcelito.

## Buscar todos los Items

- En este caso usaremos la operacion FOR y mycol.find() la cual primero buscara todos los Items, y los recorreremos con el FOR: 

**```**
        items = mycol.find()
    for Item in items:
        print(Item)
**```**

Mediante el print, se mostraran todos los items que haya encontrado el ".find()".

(NOTA: al no definir un filtrado ni un item en particular, el .find() mostrara todo su contenido)..

## Buscar algunos Items

- Para buscar algunos items en especifico deberemos crear una especie de filtro y una vez creado, lo pasaremos por el .find(). De esta manera el find se centrara en el filtro que hayamos colocado:

**```**
        filtrado_items = {"item a buscar"}

        items_especificos = mycol.find(filtrado_items)

    for Item in items_especificos:
        print(Item)       
**```**
El print de Item nos devolvera el item a buscar que hayamos elegido en el filtrado de items.

## Bonus Utility

- A veces cuando testeamos codigo en Pymongo, trabajamos con distintos items los cuales vamos agregando a medida que ejecutamos los update y las colecciones y los cargamos en la base de datos, en caso de que vayamos cargando la base de datos y querramos limpiarla para testear de manera mas ordenada o para eliminar los items que cargamos previamente, se puede utilizar un .drop() el cual limpiara la memoria de la base de datos:

**```**
mycol.drop()
**```**
