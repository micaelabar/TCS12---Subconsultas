# tarea de las Subconsultas.
## 1. El numero total de facturas realizadas por cada cliente.
 - Sentencia:
```
SELECT 
    COUNT(i.client_id)
FROM 
    invoice i
WHERE 
    i.client_id = 1;

````
-Captura.
<imag![image](https://github.com/micaelabar/TCS12---Subconsultas/assets/148156209/358e05d5-d22b-483d-8215-63f8b2e2e2d7)

## 2.Listar nombre y correo de los clientes junto a su compra mas cara realizada.
 - Sentencia:
```
SELECT 
    c.full_name,
    c.email,
    i.total AS compra_mas_cara
FROM 
    clients c
JOIN
    invoice i ON c.id = i.client_id 
WHERE 
    i.total = ( 
        SELECT MAX(i2.total)
        FROM invoice i2
        WHERE i2.client_id = c.id
    );
````
-Captura.
<imag![image](https://github.com/micaelabar/TCS12---Subconsultas/assets/148156209/ba4d9915-f93a-4184-b39b-33934473c207)

## 3. Listar las facturas donde sus totales sean mayores al promedio de las facturas
 - Sentencia:
```
SELECT i.created_at, i.total
From invoice i
WHERE i.total > (SELECT AVG(total) FROM invoice);
````
-Captura.
<imag![image](https://github.com/micaelabar/TCS12---Subconsultas/assets/148156209/e00fb228-4c71-4559-95b7-5675acfa1b9b)

#EJEMPLO CON SELECT Y WHERE.
##3. El número de facturas para cada cliente y muestra el nombre del cliente, su dirección y el total de facturas.
 - Sentencia:
```
SELECT 
    c.full_name,
    c.address,
    (SELECT COUNT(*) FROM invoice i WHERE i.client_id = c.id) AS total_facturas
FROM 
    clients c;
````
-Captura.
<imag!![Captura de pantalla 2024-07-01 110012](https://github.com/micaelabar/TCS12---Subconsultas/assets/148156209/65765daa-8e05-4f6c-9f36-d2e5c64be341)


##4. El número de facturas para cada cliente y muestra el nombre del cliente, su dirección y el total de facturas.
 - Sentencia:
```
SELECT 
    c.full_name,
    c.address
FROM 
    clients c
WHERE 
    NOT EXISTS (SELECT 1 
                FROM invoice i 
                WHERE i.client_id = c.id);
````
-Captura.
<imag!![Captura de pantalla 2024-07-01 110315](https://github.com/micaelabar/TCS12---Subconsultas/assets/148156209/ce9a8d49-b4e5-45ef-b0f1-d7bcffbe100a)


