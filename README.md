# Tarea_12_SXE

## Apartado 1

Como mencionamos en clase, aunque no es recomendable, en ocasiones puede ser necesario crear tablas ajenas a Odoo dentro de su base de datos (integración con sistemas externos, almacenamiento de históricos, datos temporales…). Mediante la herramienta PgAdmin u otro método que estimes oportuno, elabora y ejecuta una sentencia que cree una tabla llamada "EmpresasFCT" con los siguientes campos:

- **idEmpresa**: autonumérico. Este campo será la clave primaria.
- **nombre**: Texto con tamaño máximo de 40 caracteres.
- **quiereAlumnos**: Booleano.
- **numAlumnos**: Número entero.
- **fechaContacto**: Tipo fecha.

![imagen](https://github.com/user-attachments/assets/3b2f9941-3235-4ba5-bfa9-f0d3eeeec4ab)

```sql
CREATE TABLE EmpresasFct (
    IdEmpresa SERIAL PRIMARY KEY,
    nombre VARCHAR(40),
    quiereAlumnos BOOLEAN,
    numAlumnos INT,
    fechaContacto DATE
);
```

## Apartado 2

Inserta 5 registros inventados en la tabla a través de una sentencia SQL.

![imagen](https://github.com/user-attachments/assets/b27a68d2-bb7d-42ca-af04-4d84a32186cf)

```sql
INSERT INTO public.empresasfct (idempresa, nombre, quiereAlumnos, numAlumnos, fechaContacto) VALUES
    (1, 'Alcampo', true, 10, '2024-09-20'),
    (2, 'Corte Ingles', false, 0, '2024-09-22'),
    (3, 'Aldi', true, 8, '2024-09-25'),
    (4, 'Daniel Castelao', true, 2, '2024-09-29'),
    (5, 'Ies Teis', false, 0, '2024-09-30');
```

## Apartado 3

Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT ordenados por fechaContacto, de modo que en la primera fila salga el que tenga la fecha más reciente.

![imagen](https://github.com/user-attachments/assets/c2774b2f-ebae-44bf-99d1-8c406e37da91)

```sql
SELECT idempresa, nombre, quiereAlumnos, fechaContacto
FROM public.empresasfct
ORDER BY fechaContacto DESC;
```

## Apartado 4

Realiza una consulta que permita obtener un listado de todos los contactos de Odoo (no empresas) con la siguiente información:

- **Nombre**
- **Cuya ciudad sea Tracy**
- **Nombre comercial de la empresa**

Ordenados alfabéticamente por el nombre comercial de la empresa.

![imagen](https://github.com/user-attachments/assets/9ac7ee19-2302-45e0-90f6-98eeb4161dbb)

```sql
SELECT name, city, commercial_company_name 
FROM res_partner
WHERE is_company = false AND city = 'Tracy'
ORDER BY commercial_company_name;
```

## Apartado 5

Utilizando las tablas de Odoo, obtén un listado de empresas proveedoras, que han emitido algún reembolso (facturas rectificativas de proveedor):

- **Nombre de la empresa**
- **Número de factura**
- **Fecha de la factura**
- **Total factura SIN impuestos**

Ordenadas por fecha de factura de modo que la primera sea la más reciente.

![imagen](https://github.com/user-attachments/assets/945262c1-f378-45b1-a687-5488d40b66b8)

```sql
SELECT DISTINCT invoice_partner_display_name, invoice_date, amount_untaxed
FROM account_move
WHERE move_type = 'in_refund'
ORDER BY invoice_date DESC;
```

## Apartado 6

Utilizando las tablas de Odoo, obtén un listado de empresas clientes, a las que se les ha emitido más de dos facturas de venta (solo venta) confirmadas, mostrando los siguientes datos:

- **Nombre de la empresa**
- **Número de facturas**
- **Total facturado SIN IMPUESTOS**

![imagen](https://github.com/user-attachments/assets/14d1c1b6-0556-4ee1-be4d-a77c1768d53e)

```sql
SELECT invoice_partner_display_name, COUNT(DISTINCT name) AS Numero_de_facturas, 
       SUM(amount_untaxed) AS Total_facturado 
FROM account_move
WHERE move_type = 'out_invoice' AND state = 'posted'
GROUP BY invoice_partner_display_name
HAVING COUNT(DISTINCT name) > 2;
```

## Apartado 7

Crea una sentencia que actualice el correo de los contactos cuyo dominio es `@bilbao.example.com` a `@bilbao.bizkaia.eus`.

![imagen](https://github.com/user-attachments/assets/4ebc4913-25f8-4d66-a456-b87feaa7b6ab)

```sql
UPDATE res_partner
SET email = REPLACE(email, '@bilbao.example.com', '@bilbao.bizkaia.eus')
WHERE email LIKE '%@bilbao.example.com';

SELECT email FROM res_partner
WHERE email LIKE '%@bilbao.bizkaia.eus';
```

## Apartado 8

La empresa **Ready Mat** ha hecho un ERE y ha despedido a todos los empleados que tenías como contacto. Crea una sentencia que elimine todos los contactos pertenecientes a la empresa "Ready Mat", pero mantén la empresa.

Antes del borrado:

![imagen](https://github.com/user-attachments/assets/ecfe347e-86d7-4906-a29e-7aa69bac898d)

![imagen](https://github.com/user-attachments/assets/7a70e250-d419-4765-a619-d018b625d12b)

```sql
DELETE FROM res_partner
WHERE commercial_company_name = 'Ready Mat' AND is_company = false;
```

Después del borrado:

![imagen](https://github.com/user-attachments/assets/7a70e250-d419-4765-a619-d018b625d12b)
