# MySQL
> Instrucciones Basicas

### Cancelar una instruccion
Podemos cancelar una instruccion de MySQL presionando `Ctrl C`

```bash
mysql> INSERT INTO X ...^C
mysql>
```

### Obtener Bases de Datos Disponibles
```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| seven_eleven       |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```

### Crear una Base de Datos
```bash
mysql> CREATE DATABASE seven_eleven_2;
Query OK, 1 row affected (0.01 sec)
```

### Seleccionar una Base de Datos
```bash
mysql> USE seven_eleven;
Database changed
```

### Crear una Tabla
```bash
mysql> CREATE TABLE customer (
    ->   id INT(10) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    ->   first_name VARCHAR(30) NOT NULL,
    ->   last_name VARCHAR(30) NOT NULL,
    ->   email VARCHAR(60),
    ->   city VARCHAR(80)
    -> );
Query OK, 0 rows affected (0.06 sec)
```

### Obtener Descripcion de una Tabla
```bash
mysql> DESCRIBE customer;
+------------+------------------+------+-----+---------+----------------+
| Field      | Type             | Null | Key | Default | Extra          |
+------------+------------------+------+-----+---------+----------------+
| id         | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| first_name | varchar(30)      | NO   |     | NULL    |                |
| last_name  | varchar(30)      | NO   |     | NULL    |                |
| email      | varchar(60)      | YES  |     | NULL    |                |
| city       | varchar(80)      | YES  |     | NULL    |                |
+------------+------------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)
```

### Insertar un registro en una tabla
```bash
mysql> INSERT INTO customer (
    ->   first_name,
    ->   last_name,
    ->   email,
    ->   city
    -> ) VALUES (
    ->   'Esteban',
    ->   'Borai',
    ->   'estebanborai@outlook.com',
    ->   'Buenos Aires'
    -> );
Query OK, 1 row affected (0.00 sec)
```

### Seleccionar todas las columnas de una tabla
```bash
mysql> SELECT * FROM customer;
+----+------------+-----------+--------------------------+--------------+
| id | first_name | last_name | email                    | city         |
+----+------------+-----------+--------------------------+--------------+
|  1 | Esteban    | Borai     | estebanborai@outlook.com | Buenos Aires |
+----+------------+-----------+--------------------------+--------------+
1 row in set (0.00 sec)
```

### Seleccionar algunas columnas de una tabla
```bash
mysql> SELECT email, city FROM customer;
+--------------------------+--------------+
| email                    | city         |
+--------------------------+--------------+
| estebanborai@outlook.com | Buenos Aires |
+--------------------------+--------------+
1 row in set (0.00 sec)
```

### Insertar varios registros a la vez
```bash
mysql> INSERT INTO customer (
    ->   first_name,
    ->   last_name,
    ->   email,
    ->   city
    -> ) VALUES (
    ->   'Nicolas',
    ->   'Pinzon',
    ->   'neyderpinzon@outlook.com',
    ->   'Buenos Aires'
    -> ),
    -> (
    ->   'John',
    ->   'Appleseed',
    ->   'john_appleseed@mail.com',
    ->   'Palo Alto'
    -> ),
    -> (
    ->   'Mark',
    ->   'Contoso',
    ->   'mark.contoso@microsoft.com',
    ->   'San Franciso, CA'
    -> );
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

Podemos verificar nuestra tabla `customer`:

```bash
mysql> SELECT * FROM customer;
+----+------------+-----------+----------------------------+------------------+
| id | first_name | last_name | email                      | city             |
+----+------------+-----------+----------------------------+------------------+
|  1 | Esteban    | Borai     | estebanborai@outlook.com   | Buenos Aires     |
|  2 | Nicolas    | Pinzon    | neyderpinzon@outlook.com   | Buenos Aires     |
|  3 | John       | Appleseed | john_appleseed@mail.com    | Palo Alto        |
|  4 | Mark       | Contoso   | mark.contoso@microsoft.com | San Franciso, CA |
+----+------------+-----------+----------------------------+------------------+
4 rows in set (0.00 sec)
```

### Seleccionar filas con caracteristicas especificas
Seleccionamos todos las filas de la tabla `customer` donde la columna `city` sea de valor `Buenos Aires`:
```bash
mysql> SELECT * FROM customer WHERE city='Buenos Aires';
+----+------------+-----------+--------------------------+--------------+
| id | first_name | last_name | email                    | city         |
+----+------------+-----------+--------------------------+--------------+
|  1 | Esteban    | Borai     | estebanborai@outlook.com | Buenos Aires |
|  2 | Nicolas    | Pinzon    | neyderpinzon@outlook.com | Buenos Aires |
+----+------------+-----------+--------------------------+--------------+
2 rows in set (0.00 sec)
```

### Eliminar filas de una tabla
Insertaremos un registro y luego lo eliminaremos:
- Insertar registro:
```bash
mysql> INSERT INTO customer (
    ->   first_name,
    ->   last_name,
    ->   email,
    ->   city
    -> ) VALUES (
    ->   'Sarasa',
    ->   'Sarasa',
    ->   'sarasa@outlook.com',
    ->   'Sarasa'
    -> );
Query OK, 1 row affected (0.01 sec)
```

- Verificamos el registro en la tabla
```bash
mysql> SELECT * FROM customer WHERE first_name='Sarasa';
+----+------------+-----------+--------------------+--------+
| id | first_name | last_name | email              | city   |
+----+------------+-----------+--------------------+--------+
|  5 | Sarasa     | Sarasa    | sarasa@outlook.com | Sarasa |
+----+------------+-----------+--------------------+--------+
1 row in set (0.00 sec)

```

- Eliminar Registro:
```bash
mysql> DELETE FROM customer WHERE first_name='Sarasa';
Query OK, 1 row affected (0.00 sec)
```

- Verificamos que no exista en la tabla
```bash
mysql> SELECT * FROM customer WHERE first_name='Sarasa';
Empty set (0.01 sec)
```
