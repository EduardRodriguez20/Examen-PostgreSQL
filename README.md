# EXAMEN

Eduard Andres Rodriguez Holguin - Campuslands

#### Creacion

```sql
   CREATE DATABASE ventas;

   c\ ventas;

   CREATE TABLE cliente (
   id INT PRIMARY KEY,
   nombre VARCHAR(100) NOT NULL,
   apellido1 VARCHAR(100) NOT NULL,
   apellido2 VARCHAR(100),
   ciudad VARCHAR(100),
   categoría INT
   );

   CREATE TABLE comercial (
   id INT PRIMARY KEY,
   nombre VARCHAR(100) NOT NULL,
   apellido1 VARCHAR(100) NOT NULL,
   apellido2 VARCHAR(100),
   comisión FLOAT
   );

   CREATE TABLE pedido (
   id INT PRIMARY KEY,
   total FLOAT NOT NULL,
   fecha DATE,
   id_cliente INT NOT NULL REFERENCES cliente (id),
   id_comercial INT NOT NULL REFERENCES comercial(id)
   );
```

#### Poblacion

```sql
   INSERT INTO cliente VALUES(1, 'Aarón', 'Rivero', 'Gómez', 'Almería', 100);
   INSERT INTO cliente VALUES(2, 'Adela', 'Salas', 'Díaz', 'Granada', 200);
   INSERT INTO cliente VALUES(3, 'Adolfo', 'Rubio', 'Flores', 'Sevilla', NULL);
   INSERT INTO cliente VALUES(4, 'Adrián', 'Suárez', NULL, 'Jaén', 300);
   INSERT INTO cliente VALUES(5, 'Marcos', 'Loyola', 'Méndez', 'Almería', 200);
   INSERT INTO cliente VALUES(6, 'María', 'Santana', 'Moreno', 'Cádiz', 100);
   INSERT INTO cliente VALUES(7, 'Pilar', 'Ruiz', NULL, 'Sevilla', 300);
   INSERT INTO cliente VALUES(8, 'Pepe', 'Ruiz', 'Santana', 'Huelva', 200);
   INSERT INTO cliente VALUES(9, 'Guillermo', 'López', 'Gómez', 'Granada', 225);
   INSERT INTO cliente VALUES(10, 'Daniel', 'Santana', 'Loyola', 'Sevilla', 125);

   INSERT INTO comercial VALUES(1, 'Daniel', 'Sáez', 'Vega', 0.15);
   INSERT INTO comercial VALUES(2, 'Juan', 'Gómez', 'López', 0.13);
   INSERT INTO comercial VALUES(3, 'Diego','Flores', 'Salas', 0.11);
   INSERT INTO comercial VALUES(4, 'Marta','Herrera', 'Gil', 0.14);
   INSERT INTO comercial VALUES(5, 'Antonio','Carretero', 'Ortega', 0.12);
   INSERT INTO comercial VALUES(6, 'Manuel','Domínguez', 'Hernández', 0.13);
   INSERT INTO comercial VALUES(7, 'Antonio','Vega', 'Hernández', 0.11);
   INSERT INTO comercial VALUES(8, 'Alfredo','Ruiz', 'Flores', 0.05);

   INSERT INTO pedido VALUES(1, 150.5, '2017-10-05', 5, 2);
   INSERT INTO pedido VALUES(2, 270.65, '2016-09-10', 1, 5);
   INSERT INTO pedido VALUES(3, 65.26, '2017-10-05', 2, 1);
   INSERT INTO pedido VALUES(4, 110.5, '2016-08-17', 8, 3);
   INSERT INTO pedido VALUES(5, 948.5, '2017-09-10', 5, 2);
   INSERT INTO pedido VALUES(6, 2400.6, '2016-07-27', 7, 1);
   INSERT INTO pedido VALUES(7, 5760, '2015-09-10', 2, 1);
   INSERT INTO pedido VALUES(8, 1983.43, '2017-10-10', 4, 6);
   INSERT INTO pedido VALUES(9, 2480.4, '2016-10-10', 8, 3);
   INSERT INTO pedido VALUES(10, 250.45, '2015-06-27', 8, 2);
   INSERT INTO pedido VALUES(11, 75.29, '2016-08-17', 3, 7);
   INSERT INTO pedido VALUES(12, 3045.6, '2017-04-25', 2, 1);
   INSERT INTO pedido VALUES(13, 545.75, '2019-01-25', 6, 1);
   INSERT INTO pedido VALUES(14, 145.82, '2017-02-02', 6, 1);
   INSERT INTO pedido VALUES(15, 370.85, '2019-03-11', 1, 5);
   INSERT INTO pedido VALUES(16, 2389.23, '2019-03-11', 1, 5);
```

### Consultas

1. **Consultas sobre una tabla**
   1.1. Devuelve un listado con todos los pedidos que se han realizado. Los pedidos deben estar ordenados por la fecha de realización, mostrando en primer lugar los pedidos más recientes.

      ```sql
         SELECT * FROM pedido ORDER BY fecha DESC;
      ```

      Resultado:
      
      ```bash
      | id  |  total  |   fecha    | id_cliente | id_comercial |
      |---- |---------|------------|------------|--------------|
      | 16  | 2389.23 | 2019-03-11 |      1     |       5      |
      | 15  |  370.85 | 2019-03-11 |      1     |       5      |
      | 13  |  545.75 | 2019-01-25 |      6     |       1      |
      |  8  | 1983.43 | 2017-10-10 |      4     |       6      |
      |  1  |   150.5 | 2017-10-05 |      5     |       2      |
      |  3  |   65.26 | 2017-10-05 |      2     |       1      |
      |  5  |   948.5 | 2017-09-10 |      5     |       2      |
      | 12  |  3045.6 | 2017-04-25 |      2     |       1      |
      | 14  |  145.82 | 2017-02-02 |      6     |       1      |
      |  9  |  2480.4 | 2016-10-10 |      8     |       3      |
      |  2  |  270.65 | 2016-09-10 |      1     |       5      |
      | 11  |   75.29 | 2016-08-17 |      3     |       7      |
      |  4  |   110.5 | 2016-08-17 |      8     |       3      |
      |  6  |  2400.6 | 2016-07-27 |      7     |       1      |
      |  7  |    5760 | 2015-09-10 |      2     |       1      |
      | 10  |  250.45 | 2015-06-27 |      8     |       2      |
      ```

   1.2. Devuelve todos los datos de los dos pedidos de mayor valor.

      ```sql
         SELECT * FROM pedido ORDER BY fecha DESC LIMIT 2;
      ```

      Resultado:
      
      ```bash
      | id  |  total  |   fecha    | id_cliente | id_comercial |
      |-----|---------|------------|------------|--------------|
      | 15  |  370.85 | 2019-03-11 |      1     |       5      |
      | 16  | 2389.23 | 2019-03-11 |      1     |       5      |
      ```

   1.3. Devuelve un listado con los identificadores de los clientes que han realizado algún pedido. Tenga en cuenta que no debe mostrar identificadores que estén repetidos.

      ```sql
         SELECT DISTINCT c.id, c.apellido1, c.apellido2, c.nombre 
         FROM pedido p
         JOIN cliente c ON p.id_cliente = c.id ORDER BY c.id;
      ```

      Resultado:
      
      ```bash
      | id  | apellido1 | apellido2 |  nombre  |
      |-----|-----------|-----------|----------|
      |  1  |  Rivero   |   Gómez   |  Aarón   |
      |  2  |   Salas   |   Díaz    |  Adela   |
      |  3  |   Rubio   |   Flores  |  Adolfo  |
      |  4  |  Suárez   |           |  Adrián  |
      |  5  |  Loyola   |   Méndez  |  Marcos  |
      |  6  |  Santana  |   Moreno  |  María   |
      |  7  |   Ruiz    |           |  Pilar   |
      |  8  |   Ruiz    |  Santana  |   Pepe   |
      ```

   1.4. Devuelve un listado de todos los pedidos que se realizaron durante el año 2017, cuya cantidad total sea superior a 500€.

      ```sql
         SELECT * FROM pedido 
         WHERE EXTRACT(YEAR FROM fecha) = '2017' AND total > 500;
      ```

      Resultado:
      
      ```bash
      | id  |  total  |   fecha    | id_cliente | id_comercial |
      |-----|---------|------------|------------|--------------|
      |  5  |   948.5 | 2017-09-10 |      5     |       2      |
      |  8  | 1983.43 | 2017-10-10 |      4     |       6      |
      | 12  |  3045.6 | 2017-04-25 |      2     |       1      |
      ```

   1.5. Devuelve un listado con el nombre y los apellidos de los comerciales que tienen una comisión entre 0.05 y 0.11.

      ```sql
         SELECT nombre, apellido1, apellido2 
         FROM comercial WHERE comisión BETWEEN 0.05 AND 0.11;
      ```

      Resultado:
      
      ```bash
      |  nombre  | apellido1 | apellido2 |
      |----------|-----------|-----------|
      |  Diego   |   Flores  |   Salas   |
      | Antonio  |    Vega   | Hernández |
      | Alfredo  |    Ruiz   |  Flores   |

      ```

   1.6. Devuelve el valor de la comisión de mayor valor que existe en la tabla `comercial`.

      ```sql
         SELECT comisión FROM comercial ORDER BY comisión DESC LIMIT 1;
      ```

      Resultado:
      
      ```bash
      | comisión |
      |----------|
      |   0.15   |

      ```

   1.7. Devuelve el identificador, nombre y primer apellido de aquellos clientes cuyo segundo apellido **no** es `NULL`. El listado deberá estar ordenado alfabéticamente por apellidos y nombre.

      ```sql
         SELECT * FROM cliente WHERE apellido2 IS NOT NULL ORDER BY apellido1, nombre; 
      ```

      Resultado:
      
      ```bash
      | id  |   nombre  | apellido1 | apellido2 |  ciudad  | categoría |
      |-----|-----------|-----------|-----------|----------|-----------|
      |  1  |   Aarón   |   Rivero  |   Gómez   | Almería  |    100    |
      |  2  |   Adela   |   Salas   |    Díaz   | Granada  |    200    |
      |  3  |  Adolfo   |   Rubio   |   Flores  | Sevilla  |           |
      |  5  |  Marcos   |   Loyola  |   Méndez  | Almería  |    200    |
      |  6  |   María   |  Santana  |   Moreno  |  Cádiz   |    100    |
      |  8  |   Pepe    |   Ruiz    |  Santana  |  Huelva  |    200    |
      |  9  | Guillermo |   López   |   Gómez   | Granada  |    225    |
      | 10  |  Daniel   |  Santana  |   Loyola  | Sevilla  |    125    |

      ```

   1.8. Devuelve un listado de los nombres de los clientes que empiezan por `A` y terminan por `n` y también los nombres que empiezan por `P`. El listado deberá estar ordenado alfabéticamente.

      ```sql
         SELECT nombre FROM cliente 
         WHERE (nombre LIKE 'A%' AND nombre LIKE '%n') OR nombre like 'P%';
      ```

      Resultado:
      
      ```bash
      |  nombre  |
      |----------|
      |  Aarón   |
      |  Adrián  |
      |  Pilar   |
      |   Pepe   |

      ```

   1.9. Devuelve un listado de los nombres de los clientes que **no** empiezan por `A`. El listado deberá estar ordenado alfabéticamente.

      ```sql
         SELECT nombre FROM cliente 
         WHERE NOT nombre LIKE 'A%' ORDER BY nombre;
      ```

      Resultado:
      
      ```bash
      |  nombre   |
      |-----------|
      |  Daniel   |
      | Guillermo |
      |  Marcos   |
      |  María    |
      |   Pepe    |
      |  Pilar    |

      ```

   1.10. Devuelve un listado con los nombres de los comerciales que terminan por `el` o `o`. Tenga en cuenta que se deberán eliminar los nombres repetidos.

      ```sql
         SELECT DISTINCT nombre FROM comercial 
         WHERE nombre LIKE '%el' OR nombre LIKE '%o' ORDER BY nombre;
      ```

      Resultado:
      
      ```bash
      |  nombre  |
      |----------|
      | Alfredo  |
      | Antonio  |
      |  Daniel  |
      |  Diego   |
      |  Manuel  |

      ```


2. **Consultas multitabla (Composición interna)**
Resuelva todas las consultas utilizando la sintaxis de `SQL1` y `SQL2`.

   2.1. Devuelve un listado con el identificador, nombre y los apellidos de todos los clientes que han realizado algún pedido. El listado debe estar ordenado alfabéticamente y se deben eliminar los elementos repetidos.

      ```sql
         SELECT DISTINCT c.id, c.nombre, c.apellido1, c.apellido2 
         FROM pedido p
         JOIN cliente c ON p.id_cliente = c.id 
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 |
      |-----|----------|-----------|-----------|
      |  1  |  Aarón   |  Rivero   |   Gómez   |
      |  2  |  Adela   |   Salas   |    Díaz   |
      |  3  | Adolfo   |   Rubio   |   Flores  |
      |  4  |  Adrián  |  Suárez   |           |
      |  5  |  Marcos  |  Loyola   |   Méndez  |
      |  6  |  María   | Santana   |   Moreno  |
      |  8  |   Pepe   |   Ruiz    |  Santana  |
      |  7  |  Pilar   |   Ruiz    |           |
      ```

   2.2. Devuelve un listado que muestre todos los pedidos que ha realizado cada cliente. El resultado debe mostrar todos los datos de los pedidos y del cliente. El listado debe mostrar los datos de los clientes ordenados alfabéticamente.

      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2 , p.* 
         FROM pedido p
         JOIN cliente c ON p.id_cliente = c.id 
         ORDER BY c.nombre, c.apellido1, c.apellido2;

      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 | id-2 |  total  |   fecha    |
      |-----|----------|-----------|-----------|------|---------|------------|
      |  1  |  Aarón   |  Rivero   |   Gómez   |  16  | 2389.23 | 2019-03-11 |
      |  1  |  Aarón   |  Rivero   |   Gómez   |   2  |  270.65 | 2016-09-10 |
      |  1  |  Aarón   |  Rivero   |   Gómez   |  15  |  370.85 | 2019-03-11 |
      |  2  |  Adela   |   Salas   |    Díaz   |  12  | 3045.6  | 2017-04-25 |
      |  2  |  Adela   |   Salas   |    Díaz   |   3  |  65.26  | 2017-10-05 |
      |  2  |  Adela   |   Salas   |    Díaz   |   7  |  5760   | 2015-09-10 |
      |  3  |  Adolfo  |   Rubio   |   Flores  |  11  |  75.29  | 2016-08-17 |
      |  4  |  Adrián  |  Suárez   |           |   8  | 1983.43 | 2017-10-10 |
      |  5  |  Marcos  |  Loyola   |   Méndez  |   1  |  150.5  | 2017-10-05 |
      |  5  |  Marcos  |  Loyola   |   Méndez  |   5  |  948.5  | 2017-09-10 |
      |  6  |  María   | Santana   |   Moreno  |  13  | 545.75  | 2019-01-25 |
      |  6  |  María   | Santana   |   Moreno  |  14  | 145.82  | 2017-02-02 |
      |  8  |   Pepe   |   Ruiz    |  Santana  |  10  | 250.45  | 2015-06-27 |
      |  8  |   Pepe   |   Ruiz    |  Santana  |   9  | 2480.4  | 2016-10-10 |
      |  8  |   Pepe   |   Ruiz    |  Santana  |   4  |  110.5  | 2016-08-17 |
      |  7  |  Pilar   |   Ruiz    |           |   6  | 2400.6  | 2016-07-27 |

      ```

   2.3. Devuelve un listado que muestre todos los pedidos en los que ha participado un comercial. El resultado debe mostrar todos los datos de los pedidos y de los comerciales. El listado debe mostrar los datos de los comerciales ordenados alfabéticamente.

      ```sql
         SELECT c.*, p.* FROM pedido p 
         JOIN comercial c ON p.id_comercial = c.id 
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | apellido1  | apellido2  | comisión | id-2 |  total  |   fecha    | id_cliente | id_comercial |
      |------------|------------|----------|------|---------|------------|------------|--------------|
      | Carretero  |   Ortega   |   0.12   |  16  | 2389.23 | 2019-03-11 |      1     |       5      |
      | Carretero  |   Ortega   |   0.12   |  15  |  370.85 | 2019-03-11 |      1     |       5      |
      | Carretero  |   Ortega   |   0.12   |   2  |  270.65 | 2016-09-10 |      1     |       5      |
      |    Vega    | Hernández  |   0.11   |  11  |  75.29  | 2016-08-17 |      3     |       7      |
      |    Sáez    |    Vega    |   0.15   |   7  |  5760   | 2015-09-10 |      2     |       1      |
      |    Sáez    |    Vega    |   0.15   |  14  | 145.82  | 2017-02-02 |      6     |       1      |
      |    Sáez    |    Vega    |   0.15   |  13  | 545.75  | 2019-01-25 |      6     |       1      |
      |    Sáez    |    Vega    |   0.15   |  12  | 3045.6  | 2017-04-25 |      2     |       1      |
      |    Sáez    |    Vega    |   0.15   |   3  |  65.26  | 2017-10-05 |      2     |       1      |
      |    Sáez    |    Vega    |   0.15   |   6  | 2400.6  | 2016-07-27 |      7     |       1      |
      |   Flores   |   Salas    |   0.11   |   9  | 2480.4  | 2016-10-10 |      8     |       3      |
      |   Flores   |   Salas    |   0.11   |   4  |  110.5  | 2016-08-17 |      8     |       3      |
      |   Gómez    |   López    |   0.13   |  10  | 250.45  | 2015-06-27 |      8     |       2      |
      |   Gómez    |   López    |   0.13   |   1  |  150.5  | 2017-10-05 |      5     |       2      |
      |   Gómez    |   López    |   0.13   |   5  |  948.5  | 2017-09-10 |      5     |       2      |
      | Domínguez  | Hernández  |   0.13   |   8  | 1983.43 | 2017-10-10 |      4     |       6      |

      ```

   2.4. Devuelve un listado que muestre todos los clientes, con todos los pedidos que han realizado y con los datos de los comerciales asociados a cada pedido.

      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2 , p.*, 
         co.nombre AS nombre_comercial, co.apellido1 AS apellido_comercial, 
         co.apellido2 AS apellido2_comercial 
         FROM pedido p JOIN cliente c ON p.id_cliente = c.id 
         JOIN comercial co ON p.id_comercial = co.id
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 | id-2 |  total  |   fecha    |
      |-----|----------|-----------|-----------|------|---------|------------|
      |  1  |  Aarón   |  Rivero   |   Gómez   |  16  | 2389.23 | 2019-03-11 |
      |  1  |  Aarón   |  Rivero   |   Gómez   |   2  |  270.65 | 2016-09-10 |
      |  1  |  Aarón   |  Rivero   |   Gómez   |  15  |  370.85 | 2019-03-11 |
      |  2  |  Adela   |   Salas   |    Díaz   |  12  | 3045.6  | 2017-04-25 |
      |  2  |  Adela   |   Salas   |    Díaz   |   3  |  65.26  | 2017-10-05 |
      |  2  |  Adela   |   Salas   |    Díaz   |   7  |  5760   | 2015-09-10 |
      |  3  |  Adolfo  |   Rubio   |   Flores  |  11  |  75.29  | 2016-08-17 |
      |  4  |  Adrián  |  Suárez   |           |   8  | 1983.43 | 2017-10-10 |
      |  5  |  Marcos  |  Loyola   |   Méndez  |   1  |  150.5  | 2017-10-05 |
      |  5  |  Marcos  |  Loyola   |   Méndez  |   5  |  948.5  | 2017-09-10 |
      |  6  |  María   | Santana   |   Moreno  |  13  | 545.75  | 2019-01-25 |
      |  6  |  María   | Santana   |   Moreno  |  14  | 145.82  | 2017-02-02 |
      |  8  |   Pepe   |   Ruiz    |  Santana  |  10  | 250.45  | 2015-06-27 |
      |  8  |   Pepe   |   Ruiz    |  Santana  |   9  | 2480.4  | 2016-10-10 |
      |  8  |   Pepe   |   Ruiz    |  Santana  |   4  |  110.5  | 2016-08-17 |
      |  7  |  Pilar   |   Ruiz    |           |   6  | 2400.6  | 2016-07-27 |

      ```

   2.5. Devuelve un listado de todos los clientes que realizaron un pedido durante el año `2017`, cuya cantidad esté entre `300` € y `1000` €.

      ```sql
         SELECT c.*, p.* FROM pedido p
         JOIN cliente c ON p.id_cliente = c.id
         WHERE EXTRACT(YEAR FROM p.fecha) = '2017' 
         AND p.total BETWEEN 300 AND 1000;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 |  ciudad  | categoría | id-2 |
      |-----|----------|-----------|-----------|----------|-----------|------|
      |  5  |  Marcos  |  Loyola   |   Méndez  | Almería  |    200    |   5  |

      ```

   2.6. Devuelve el nombre y los apellidos de todos los comerciales que ha participado en algún pedido realizado por `María Santana Moreno`.

      ```sql
         SELECT DISTINCT co.nombre, co.apellido1, co.apellido2 FROM pedido p 
         JOIN cliente c ON p.id_cliente = c.id 
         JOIN comercial co ON p.id_comercial = co.id
         WHERE c.id = 6;
      ```

      Resultado:
      
      ```bash
      |  nombre  | apellido1 | apellido2 |
      |----------|-----------|-----------|
      |  Daniel  |    Sáez   |    Vega   |

      ```
   
   2.7. Devuelve el nombre de todos los clientes que han realizado algún pedido con el comercial `Daniel Sáez Vega`.

      ```sql
         SELECT DISTINCT c.nombre, c.apellido1, c.apellido2 FROM pedido p 
         JOIN cliente c ON p.id_cliente = c.id 
         JOIN comercial co ON p.id_comercial = co.id
         WHERE co.id = 1;
      ```

      Resultado:
      
      ```bash
      |  nombre  | apellido1 | apellido2 |
      |----------|-----------|-----------|
      |  Adela   |   Salas   |    Díaz   |
      |  María   |  Santana  |   Moreno  |
      |  Pilar   |   Ruiz    |           |

      ```



3. **Consultas multitabla (Composición externa)**
Resuelva todas las consultas utilizando las cláusulas `LEFT JOIN` y `RIGHT JOIN`.

   3.1. Devuelve un listado con **todos los clientes** junto con los datos de los pedidos que han realizado. Este listado también debe incluir los clientes que no han realizado ningún pedido. El listado debe estar ordenado alfabéticamente por el primer apellido, segundo apellido y nombre de los clientes.

      ```sql
         SELECT * FROM cliente c
         LEFT JOIN pedido p ON c.id = p.id_cliente
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 |  ciudad  | categoría | id-2 |
      |-----|----------|-----------|-----------|----------|-----------|------|
      |  1  |  Aarón   |  Rivero   |   Gómez   | Almería  |    100    |  15  |
      |  1  |  Aarón   |  Rivero   |   Gómez   | Almería  |    100    |   2  |
      |  1  |  Aarón   |  Rivero   |   Gómez   | Almería  |    100    |  16  |
      |  2  |  Adela   |   Salas   |    Díaz   | Granada  |    200    |   7  |
      |  2  |  Adela   |   Salas   |    Díaz   | Granada  |    200    |  12  |
      |  2  |  Adela   |   Salas   |    Díaz   | Granada  |    200    |   3  |
      |  3  |  Adolfo  |   Rubio   |   Flores  | Sevilla  |           |  11  |
      |  4  |  Adrián  |  Suárez   |           |   Jaén   |    300    |   8  |
      | 10  |  Daniel  |  Santana  |   Loyola  | Sevilla  |    125    |      |
      |  9  | Guillermo|   López   |   Gómez   | Granada  |    225    |      |
      |  5  |  Marcos  |  Loyola   |   Méndez  | Almería  |    200    |   1  |
      |  5  |  Marcos  |  Loyola   |   Méndez  | Almería  |    200    |   5  |
      |  6  |  María   |  Santana  |   Moreno  |  Cádiz   |    100    |  13  |
      |  6  |  María   |  Santana  |   Moreno  |  Cádiz   |    100    |  14  |
      |  8  |   Pepe   |   Ruiz    |  Santana  |  Huelva  |    200    |  10  |
      |  8  |   Pepe   |   Ruiz    |  Santana  |  Huelva  |    200    |   9  |
      |  8  |   Pepe   |   Ruiz    |  Santana  |  Huelva  |    200    |   4  |
      |  7  |  Pilar   |   Ruiz    |           | Sevilla  |    300    |   6  |

      ```

   3.2. Devuelve un listado con **todos los comerciales** junto con los datos de los pedidos que han realizado. Este listado también debe incluir los comerciales que no han realizado ningún pedido. El listado debe estar ordenado alfabéticamente por el primer apellido, segundo apellido y nombre de los comerciales.

      ```sql
         SELECT * FROM comercial c
         LEFT JOIN pedido p ON c.id = p.id_comercial
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 | comisión | id-2 |  total  |
      |-----|----------|-----------|-----------|----------|------|---------|
      |  8  |  Alfredo |   Ruiz    |   Flores  |   0.05   |      |         |
      |  5  |  Antonio | Carretero |   Ortega  |   0.12   |  15  |  370.85 |
      |  5  |  Antonio | Carretero |   Ortega  |   0.12   |  16  | 2389.23 |
      |  5  |  Antonio | Carretero |   Ortega  |   0.12   |   2  |  270.65 |
      |  7  |  Antonio |    Vega   | Hernández |   0.11   |  11  |  75.29  |
      |  1  |  Daniel  |    Sáez   |    Vega   |   0.15   |  13  | 545.75  |
      |  1  |  Daniel  |    Sáez   |    Vega   |   0.15   |   6  | 2400.6  |
      |  1  |  Daniel  |    Sáez   |    Vega   |   0.15   |   7  |  5760   |
      |  1  |  Daniel  |    Sáez   |    Vega   |   0.15   |  12  | 3045.6  |
      |  1  |  Daniel  |    Sáez   |    Vega   |   0.15   |  14  | 145.82  |
      |  1  |  Daniel  |    Sáez   |    Vega   |   0.15   |   3  |  65.26  |
      |  3  |  Diego   |   Flores  |   Salas   |   0.11   |   9  | 2480.4  |
      |  3  |  Diego   |   Flores  |   Salas   |   0.11   |   4  |  110.5  |
      |  2  |   Juan   |   Gómez   |   López   |   0.13   |   1  |  150.5  |
      |  2  |   Juan   |   Gómez   |   López   |   0.13   |   5  |  948.5  |
      |  2  |   Juan   |   Gómez   |   López   |   0.13   |  10  | 250.45  |
      |  6  |  Manuel  | Domínguez | Hernández |   0.13   |   8  | 1983.43 |
      |  4  |  Marta   |  Herrera  |    Gil    |   0.14   |      |         |

      ```

   3.3. Devuelve un listado que solamente muestre los clientes que no han realizado ningún pedido.

      ```sql
         SELECT * FROM cliente c
         LEFT JOIN pedido p ON c.id = p.id_cliente
         WHERE p.id IS NULL
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre   | apellido1 | apellido2 |  ciudad  | categoría | id-2 |
      |-----|-----------|-----------|-----------|----------|-----------|------|
      | 10  |  Daniel   |  Santana  |  Loyola   | Sevilla  |    125    |      |
      |  9  | Guillermo |   López   |   Gómez   | Granada  |    225    |      |

      ```

   3.4. Devuelve un listado que solamente muestre los comerciales que no han realizado ningún pedido.
   
      ```sql
         SELECT * FROM comercial c
         LEFT JOIN pedido p ON c.id = p.id_comercial
         WHERE p.id IS NULL
         ORDER BY c.nombre, c.apellido1, c.apellido2;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 | comisión | id-2 | total |
      |-----|----------|-----------|-----------|----------|------|-------|
      |  8  | Alfredo  |   Ruiz    |   Flores  |   0.05   |      |       |
      |  4  |  Marta   |  Herrera  |    Gil    |   0.14   |      |       |

      ```
   
   3.5. Devuelve un listado con los clientes que no han realizado ningún pedido y de los comerciales que no han participado en ningún pedido. Ordene el listado alfabéticamente por los apellidos y el nombre. En en listado deberá diferenciar de algún modo los clientes y los comerciales.
   
      ```sql
         SELECT c.apellido1, c.apellido2, c.nombre, 'Cliente' AS tipo
         FROM cliente c
         LEFT JOIN pedido p ON c.id = p.id_cliente
         WHERE p.id IS NULL
         UNION
         SELECT co.apellido1, co.apellido2, co.nombre, 'Comercial' AS tipo
         FROM comercial co
         LEFT JOIN pedido p ON co.id = p.id_comercial
         WHERE p.id IS NULL;
      ```

      Resultado:
      
      ```bash
      | apellido1 | apellido2 |  nombre   |   tipo    |
      |-----------|-----------|-----------|-----------|
      |   López   |   Gómez   | Guillermo |  Cliente  |
      |  Santana  |  Loyola   |  Daniel   |  Cliente  |
      |   Ruiz    |   Flores  |  Alfredo  | Comercial |
      |  Herrera  |    Gil    |   Marta   | Comercial |

      ```

   3.6. ¿Se podrían realizar las consultas anteriores con `NATURAL LEFT JOIN` o `NATURAL RIGHT JOIN`? Justifique su respuesta.

      ```sql
         -- No se puede usar NATURAL JOIN puesto que para distinguir los clientes de los comerciales debemos
         -- hacer 2 consultas, si no fuera asi el NATURAL JOIN permitiria traer a los comerciales y clientes
         -- para hacer su validacion con la tabla pedidos, debido a eso hay que usar los JOIN normales.
      ```

4. **Consultas resumen**

   4.1. Calcula la cantidad total que suman todos los pedidos que aparecen en la tabla `pedido`.
   
      ```sql
         SELECT SUM(total) AS total_pedidos FROM pedido;
      ```

      Resultado:
      
      ```bash
      | total_pedidos |
      |---------------|
      |   20992.83    |

      ```

   4.2. Calcula la cantidad media de todos los pedidos que aparecen en la tabla `pedido`.
   
      ```sql
         SELECT AVG(total) AS promedio_pedidos FROM pedido;
      ```

      Resultado:
      
      ```bash
      | promedio_pedidos |
      |------------------|
      |    1312.05       |

      ```

   4.3. Calcula el número total de comerciales distintos que aparecen en la tabla `pedido`.
   
      ```sql
         SELECT COUNT(DISTINCT id_comercial) AS total_comerciantes 
         FROM pedido;
      ```

      Resultado:
      
      ```bash
      | total_comerciantes |
      |--------------------|
      |          6         |

      ```
   
   4.4. Calcula el número total de clientes que aparecen en la tabla `cliente`.
   
      ```sql
         SELECT COUNT(id) AS cantidad_clientes FROM cliente;
      ```

      Resultado:
      
      ```bash
      | cantidad_clientes |
      |-------------------|
      |         10        |

      ```
   
   4.5. Calcula cuál es la mayor cantidad que aparece en la tabla `pedido`.
   
      ```sql
         SELECT MAX(total) FROM pedido; 
      ```

      Resultado:
      
      ```bash
      | max |
      |-----|
      | 5760|

      ```
   
   4.6. Calcula cuál es la menor cantidad que aparece en la tabla `pedido`.
   
      ```sql
         SELECT MIN(total) FROM pedido;
      ```

      Resultado:
      
      ```bash
      |  min  |
      |-------|
      | 65.26 |

      ```
      
   4.7. Calcula cuál es el valor máximo de categoría para cada una de las ciudades que aparece en la tabla `cliente`.
   
      ```sql
         SELECT ciudad, MAX(categoría) FROM cliente GROUP BY ciudad;
      ```

      Resultado:
      
      ```bash
      |  ciudad  | max  |
      |----------|------|
      | Almería  |  200 |
      |  Huelva  |  200 |
      | Sevilla  |  300 |
      | Granada  |  225 |
      |   Jaén   |  300 |
      |  Cádiz   |  100 |

      ```

   4.8. Calcula cuál es el máximo valor de los pedidos realizados durante el mismo día para cada uno de los clientes. Es decir, el mismo cliente puede haber realizado varios pedidos de diferentes cantidades el mismo día. Se pide que se calcule cuál es el pedido de máximo valor para cada uno de los días en los que un cliente ha realizado un pedido. Muestra el identificador del cliente, nombre, apellidos, la fecha y el valor de la cantidad.
   
      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2, 
         p.fecha, MAX(p.total) AS total
         FROM pedido p
         JOIN cliente c ON p.id_cliente = c.id
         GROUP BY p.fecha, c.id
         ORDER BY fecha, total, c.nombre, c.apellido1, c.apellido2 DESC;
      ```

      Resultado:
      
      ```bash
      | id  |  nombre   | apellido1 | apellido2 |    fecha    |  total  |
      |-----|-----------|-----------|-----------|-------------|---------|
      |  8  |   Pepe    |    Ruiz   |  Santana  |  2015-06-27 |  250.45 |
      |  2  |   Adela   |   Salas   |    Díaz   |  2015-09-10 |  5760   |
      |  7  |   Pilar   |    Ruiz   |           |  2016-07-27 |  2400.6 |
      |  3  |  Adolfo   |   Rubio   |  Flores   |  2016-08-17 |  75.29  |
      |  8  |   Pepe    |    Ruiz   |  Santana  |  2016-08-17 |  110.5  |
      |  1  |   Aarón   |   Rivero  |   Gómez   |  2016-09-10 | 270.65  |
      |  8  |   Pepe    |    Ruiz   |  Santana  |  2016-10-10 | 2480.4  |
      |  6  |   María   |  Santana  |  Moreno   |  2017-02-02 | 145.82  |
      |  2  |   Adela   |   Salas   |    Díaz   |  2017-04-25 | 3045.6  |
      |  5  |  Marcos   |   Loyola  |  Méndez   |  2017-09-10 |  948.5  |
      |  2  |   Adela   |   Salas   |    Díaz   |  2017-10-05 |  65.26  |
      |  5  |  Marcos   |   Loyola  |  Méndez   |  2017-10-05 |  150.5  |
      |  4  |  Adrián   |  Suárez   |           |  2017-10-10 | 1983.43 |
      |  6  |   María   |  Santana  |  Moreno   |  2019-01-25 | 545.75  |
      |  1  |   Aarón   |   Rivero  |   Gómez   |  2019-03-11 | 2389.23 |

      ```

   4.9. Calcula cuál es el máximo valor de los pedidos realizados durante el mismo día para cada uno de los clientes, teniendo en cuenta que sólo queremos mostrar aquellos pedidos que superen la cantidad de 2000 €.
   
      ```sql
         SELECT fecha, MAX(total) FROM pedido 
         GROUP BY fecha HAVING MAX(total) > 2000 ORDER BY fecha;
      ```

      Resultado:
      
      ```bash
      |    fecha    |   max   |
      |-------------|---------|
      | 2015-09-10  |   5760  |
      | 2016-07-27  |  2400.6 |
      | 2016-10-10  |  2480.4 |
      | 2017-04-25  |  3045.6 |
      | 2019-03-11  | 2389.23 |

      ```

   4.10. Calcula el máximo valor de los pedidos realizados para cada uno de los comerciales durante la fecha `2016-08-17`. Muestra el identificador del comercial, nombre, apellidos y total.
   
      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2, MAX(p.total) 
         FROM pedido p
         JOIN comercial c ON p.id_comercial = c.id
         GROUP BY p.fecha, c.id HAVING p.fecha = '2016-08-17'
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 |   max   |
      |-----|----------|-----------|-----------|---------|
      |  3  |  Diego   |  Flores   |   Salas   |  110.5  |
      |  7  | Antonio  |   Vega    | Hernández |  75.29  |

      ```

   4.11. Devuelve un listado con el identificador de cliente, nombre y apellidos y el número total de pedidos que ha realizado cada uno de clientes. Tenga en cuenta que pueden existir clientes que no han realizado ningún pedido. Estos clientes también deben aparecer en el listado indicando que el número de pedidos realizados es `0`.
   
      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2, 
         COUNT(p.id) AS cantidad_pedidos 
         FROM cliente c
         LEFT JOIN pedido p ON c.id = p.id_cliente
         GROUP BY c.id ORDER BY cantidad_pedidos DESC
      ```

      Resultado:
      
      ```bash
      | id  |  nombre   | apellido1 | apellido2 | cantidad_pedidos |
      |-----|-----------|-----------|-----------|------------------|
      |  8  |   Pepe    |    Ruiz   |  Santana  |        3         |
      |  1  |   Aarón   |   Rivero  |   Gómez   |        3         |
      |  2  |   Adela   |   Salas   |    Díaz   |        3         |
      |  6  |   María   |  Santana  |  Moreno   |        2         |
      |  5  |  Marcos   |   Loyola  |  Méndez   |        2         |
      |  7  |   Pilar   |    Ruiz   |           |        1         |
      |  4  |  Adrián   |  Suárez   |           |        1         |
      |  3  |  Adolfo   |   Rubio   |  Flores   |        1         |
      |  9  | Guillermo |   López   |   Gómez   |        0         |
      | 10  |  Daniel   |  Santana  |  Loyola   |        0         |

      ```

   4.12. Devuelve un listado con el identificador de cliente, nombre y apellidos y el número total de pedidos que ha realizado cada uno de clientes **durante el año 2017**.
   
      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2, 
         COUNT(p.id) AS cantidad_pedidos 
         FROM cliente c
         LEFT JOIN pedido p ON c.id = p.id_cliente
         GROUP BY c.id, p.fecha HAVING EXTRACT(YEAR FROM p.fecha) = '2017' 
         ORDER BY cantidad_pedidos DESC
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 | cantidad_pedidos |
      |-----|----------|-----------|-----------|------------------|
      |  2  |  Adela   |   Salas   |    Díaz   |        1         |
      |  2  |  Adela   |   Salas   |    Díaz   |        1         |
      |  4  |  Adrián  |  Suárez   |           |        1         |
      |  5  |  Marcos  |   Loyola  |  Méndez   |        1         |
      |  5  |  Marcos  |   Loyola  |  Méndez   |        1         |
      |  6  |  María   |  Santana  |  Moreno   |        1         |

      ```

   4.13. Devuelve un listado que muestre el identificador de cliente, nombre, primer apellido y el valor de la máxima cantidad del pedido realizado por cada uno de los clientes. El resultado debe mostrar aquellos clientes que no han realizado ningún pedido indicando que la máxima cantidad de sus pedidos realizados es `0`. Puede hacer uso de la función `[IFNULL]`.
   
      ```sql
         SELECT c.id, c.nombre, c.apellido1, c.apellido2, 
         COALESCE(MAX(p.total), 0) AS total
         FROM cliente c
         LEFT JOIN pedido p ON c.id = p.id_cliente
         GROUP BY c.id
         ORDER BY c.id, total DESC
      ```

      Resultado:
      
      ```bash
      | id  |  nombre   | apellido1 | apellido2 |  total  |
      |-----|-----------|-----------|-----------|---------|
      |  1  |   Aarón   |   Rivero  |   Gómez   | 2389.23 |
      |  2  |   Adela   |   Salas   |    Díaz   |   5760  |
      |  3  |  Adolfo   |   Rubio   |  Flores   |  75.29  |
      |  4  |  Adrián   |  Suárez   |           | 1983.43 |
      |  5  |  Marcos   |   Loyola  |  Méndez   |  948.5  |
      |  6  |   María   |  Santana  |  Moreno   | 545.75  |
      |  7  |   Pilar   |    Ruiz   |           | 2400.6  |
      |  8  |   Pepe    |    Ruiz   |  Santana  | 2480.4  |
      |  9  | Guillermo |   López   |   Gómez   |    0    |
      | 10  |  Daniel   |  Santana  |  Loyola   |    0    |

      ```

   4.14. Devuelve cuál ha sido el pedido de máximo valor que se ha realizado cada año.
   
      ```sql
         SELECT EXTRACT(YEAR FROM fecha), MAX(total) FROM pedido 
         GROUP BY EXTRACT(YEAR FROM fecha)
      ```

      Resultado:
      
      ```bash
      | extract |    max    |
      |---------|-----------|
      |  2017   |   3045.6  |
      |  2016   |   2480.4  |
      |  2019   |  2389.23  |
      |  2015   |   5760    |

      ```

   4.15. Devuelve el número total de pedidos que se han realizado cada año.

      ```sql
         SELECT EXTRACT(YEAR FROM fecha), COUNT(id) FROM pedido 
         GROUP BY EXTRACT(YEAR FROM fecha)
      ```

      Resultado:
      
      ```bash
      | extract | count |
      |---------|-------|
      |  2017   |   6   |
      |  2016   |   5   |
      |  2019   |   3   |
      |  2015   |   2   |

      ```


5. **Con operadores básicos de comparación**

   5.1. Devuelve un listado con todos los pedidos que ha realizado `Adela Salas Díaz`. (Sin utilizar `INNER JOIN`).
   
      ```sql
         SELECT * FROM pedido
         WHERE id_cliente = (
         SELECT id FROM cliente 
         WHERE nombre = 'Adela' AND apellido1 = 'Salas' AND apellido2 = 'Díaz'
         );
      ```

      Resultado:
      
      ```bash
      | id  |  total  |   fecha    | id_cliente | id_comercial |
      |-----|---------|------------|------------|--------------|
      |  3  |  65.26  | 2017-10-05 |     2      |      1       |
      |  7  |  5760   | 2015-09-10 |     2      |      1       |
      | 12  | 3045.6  | 2017-04-25 |     2      |      1       |

      ```

   5.2. Devuelve el número de pedidos en los que ha participado el comercial `Daniel Sáez Vega`. (Sin utilizar `INNER JOIN`)
   
      ```sql
         SELECT * FROM pedido
         WHERE id_comercial = (
         SELECT id FROM comercial 
         WHERE nombre = 'Daniel' AND apellido1 = 'Sáez' AND apellido2 = 'Vega'
         );
      ```

      Resultado:
      
      ```bash
      | id  |  total  |   fecha    | id_cliente | id_comercial |
      |-----|---------|------------|------------|--------------|
      |  3  |  65.26  | 2017-10-05 |     2      |      1       |
      |  6  | 2400.6  | 2016-07-27 |     7      |      1       |
      |  7  |  5760   | 2015-09-10 |     2      |      1       |
      | 12  | 3045.6  | 2017-04-25 |     2      |      1       |
      | 13  | 545.75  | 2019-01-25 |     6      |      1       |
      | 14  | 145.82  | 2017-02-02 |     6      |      1       |

      ```

   5.3. Devuelve los datos del cliente que realizó el pedido más caro en el año `2019`. (Sin utilizar `INNER JOIN`)
   
      ```sql
         SELECT * FROM cliente
         WHERE id = (
         SELECT id_cliente FROM pedido
         WHERE EXTRACT(YEAR FROM fecha) = '2019' 
         ORDER BY total DESC LIMIT 1
         );
      ```

      Resultado:
      
      ```bash
      | id  | nombre | apellido1 | apellido2 |  ciudad  | categoría |
      |-----|--------|-----------|-----------|----------|-----------|
      |  1  | Aarón  |  Rivero   |   Gómez   | Almería  |    100    |

      ```

   5.4. Devuelve la fecha y la cantidad del pedido de menor valor realizado por el cliente `Pepe Ruiz Santana`.
   
      ```sql
         SELECT fecha, total FROM pedido
         WHERE id_cliente = (
         SELECT id FROM cliente 
         WHERE nombre = 'Pepe' AND apellido1 = 'Ruiz' 
         AND apellido2 = 'Santana'
         ) ORDER BY total ASC LIMIT 1;
      ```

      Resultado:
      
      ```bash
      |   fecha   |  total  |
      |------------|---------|
      | 2016-08-17 |  110.5  |

      ```

   5.5. Devuelve un listado con los datos de los clientes y los pedidos, de todos los clientes que han realizado un pedido durante el año `2017` con un valor mayor o igual al valor medio de los pedidos realizados durante ese mismo año.
   
      ```sql
         SELECT c.id, c.apellido1, c.apellido2, c.nombre, 
         'Cliente' AS tipo
         FROM pedido p
         JOIN cliente c ON p.id_cliente = c.id
         WHERE total >= (
         SELECT AVG(total) FROM pedido)
         UNION
         SELECT c.id, c.apellido1, c.apellido2, c.nombre, 
         'Comercial' AS tipo
         FROM pedido p
         JOIN comercial c ON p.id_comercial = c.id
         WHERE total >= (
         SELECT AVG(total) FROM pedido
         );
      ```

      Resultado:
      
      ```bash
      | id  | apellido1  | apellido2 |  nombre  |   tipo   |
      |-----|------------|-----------|----------|----------|
      |  8  |    Ruiz    |  Santana  |   Pepe   |  Cliente |
      |  3  |   Flores   |   Salas   |  Diego   | Comercial|
      |  4  |   Suárez   |           |  Adrián  |  Cliente |
      |  1  |   Rivero   |   Gómez   |  Aarón   |  Cliente |
      |  7  |    Ruiz    |           |  Pilar   |  Cliente |
      |  5  | Carretero  |   Ortega  | Antonio  | Comercial|
      |  6  | Domínguez  | Hernandez |  Manuel  | Comercial|
      |  1  |    Sáez    |    Vega   |  Daniel  | Comercial|
      |  2  |    Salas   |    Díaz   |  Adela   |  Cliente |

      ```

6. **Subconsultas con `ALL` y `ANY`**

   6.1. Devuelve el pedido más caro que existe en la tabla `pedido` si hacer uso de `MAX`, `ORDER BY` ni `LIMIT`.
   
      ```sql
         SELECT * FROM pedido 
         WHERE total >= ALL (SELECT total FROM pedido)
      ```

      Resultado:
      
      ```bash
      | id  | total |   fecha    | id_cliente | id_comercial |
      |-----|-------|------------|------------|--------------|
      |  7  |  5760 | 2015-09-10 |     2      |       1      |

      ```

   6.2. Devuelve un listado de los clientes que no han realizado ningún pedido. (Utilizando `ANY` o `ALL`).
   
      ```sql
         SELECT * FROM cliente
         WHERE NOT id = ANY (SELECT id_cliente FROM pedido)
      ```

      Resultado:
      
      ```bash
      | id  |   nombre   | apellido1 | apellido2 |  ciudad  | categoría |
      |-----|------------|-----------|-----------|----------|-----------|
      |  9  | Guillermo  |   López   |   Gómez   | Granada  |    225    |
      | 10  |   Daniel   |  Santana  |   Loyola  | Sevilla  |    125    |

      ```

   6.3. Devuelve un listado de los comerciales que no han realizado ningún pedido. (Utilizando `ANY` o `ALL`).

      ```sql
         SELECT * FROM comercial
         WHERE NOT id = ANY (SELECT id_comercial FROM pedido)
      ```

      Resultado:
      
      ```bash
      | id  |  nombre  | apellido1 | apellido2 | comisión |
      |-----|----------|-----------|-----------|----------|
      |  4  |  Marta   |  Herrera  |    Gil    |   0.14   |
      |  8  | Alfredo  |    Ruiz   |   Flores  |   0.05   |

      ```

7. **Subconsultas con `IN` y `NOT IN`**

   7.1. Devuelve un listado de los clientes que no han realizado ningún pedido. (Utilizando `IN` o `NOT IN`).
   
      ```sql
         SELECT * FROM cliente 
         WHERE NOT id IN (SELECT id_cliente FROM pedido)
      ```

      Resultado:
      
      ```bash
      | id  |   nombre   | apellido1 | apellido2 |  ciudad  | categoría |
      |-----|------------|-----------|-----------|----------|-----------|
      |  9  | Guillermo  |   López   |   Gómez   | Granada  |    225    |
      | 10  |   Daniel   |  Santana  |   Loyola  | Sevilla  |    125    |

      ```

   7.2. Devuelve un listado de los comerciales que no han realizado ningún pedido. (Utilizando `IN` o `NOT IN`).

      ```sql
         SELECT * FROM comercial
         WHERE NOT id IN (SELECT id_comercial FROM pedido)
      ```

      Resultado:
      
      ```bash
      | id |  nombre  | apellido1 | apellido2 | comisión |
      |----|----------|-----------|-----------|----------|
      |  4 |  Marta   |  Herrera  |    Gil    |   0.14   |
      |  8 | Alfredo  |    Ruiz   |   Flores  |   0.05   |

      ```


8. **Subconsultas con `EXISTS` y `NOT EXISTS`**

   8.1. Devuelve un listado de los clientes que no han realizado ningún pedido. (Utilizando `EXISTS` o `NOT EXISTS`).

      ```sql
         SELECT * FROM cliente c
         WHERE NOT EXISTS (
            SELECT 1 FROM pedido p WHERE p.id_cliente = c.id
         );
      ```

      Resultado:
      
      ```bash
      | id |  nombre    | apellido1 | apellido2 |  ciudad  | categoría |
      |----|------------|-----------|-----------|----------|-----------|
      | 10 |  Daniel    |  Santana  |   Loyola  | Sevilla  |    125    |
      |  9 | Guillermo  |   López   |   Gómez   | Granada  |    225    |

      ```

   8.2. Devuelve un listado de los comerciales que no han realizado ningún pedido. (Utilizando `EXISTS` o `NOT EXISTS`).

      ```sql
         SELECT * FROM comercial c
         WHERE NOT EXISTS (
         SELECT 1 FROM pedido p WHERE p.id_comercial = c.id
         );
      ```

      Resultado:
      
      ```bash
      | id |  nombre  | apellido1 | apellido2 | comisión |
      |----|----------|-----------|-----------|----------|
      |  8 | Alfredo  |    Ruiz   |   Flores  |   0.05   |
      |  4 |  Marta   |  Herrera  |    Gil    |   0.14   |

      ```

