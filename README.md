# Tarea_12_SXE

Apartado 1

Como mencionamos en clase, aunque no es recomendable, en ocasiones puede ser
necesario crear tablas ajenas a Odoo dentro de su base de datos (integración con
sistemas externos, almacenamiento de históricos, datos temporales…). Mediante la
herramienta PgAdmin u otro método que estimes oportuno, elabora y ejecuta una
sentencia que cree una tabla llamada “EmpresasFCT“con los siguientes campos:

● idEmpresa: autonumérico. Este campo será la clave primaria.
● nombre: Texto con tamaño máximo de 40 caracteres.
● quiereAlumnos: Booleano.
● numAlumnos: número entero.
● fechaContacto: tipo fecha

![imagen](https://github.com/user-attachments/assets/3b2f9941-3235-4ba5-bfa9-f0d3eeeec4ab)

CREATE TABLE EmpresasFct (
	IdEmpresa Int Primary Key,
	nombre varchar(40),
	quiereAlumnos boolean,
	numAlumnos Int,
	fechaContacto Date
)


Apartado 2

Inserta 5 registros inventados en la tabla a través de una sentencia SQL.

![imagen](https://github.com/user-attachments/assets/b27a68d2-bb7d-42ca-af04-4d84a32186cf)

INSERT INTO public.empresasfct(idempresa, nombre, quiere alumnos, numalumnos, fechacontacto)Values
	(1, 'Alcampo', true, 10, '2024/09/20'),
	(2, 'Corte Ingles', False, 0, '2024/09/22'),
	(3, 'Aldi', true, 8, '2024/09/25'),
	(4, 'Daniel Castelao', true, 2, '2024/09/29'),
	(5, 'Ies Teis', false, 0, '2024/09/30');

Apartado 3

Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT
ordenados por fechaContacto, de modo que en la primera fila salga el que tenga la
fecha más reciente.

![imagen](https://github.com/user-attachments/assets/c2774b2f-ebae-44bf-99d1-8c406e37da91)

Select idempresa, nombre, quierealumnos, fechacontacto
	FROM public.empresasfct
	Order by fechacontacto DESC;

Apartado 4

Realiza una consulta que permita obtener un listado de todos los contactos de
Odoo (no empresas) con la siguiente información:

- Nombre
- Cuya ciudad sea Tracy
- Nombre comercial de la empresa
  
Ordenados alfabéticamente por el nombre comercial de la empresa.

![imagen](https://github.com/user-attachments/assets/9ac7ee19-2302-45e0-90f6-98eeb4161dbb)

Select name, city, commercial_company_name from res_partner
where is_company=false AND city='Tracy'
order by commercial_company_name

Apartado 5

Utilizando las tablas de odoo, obtén un listado de empresas proveedoras, que han
emitido algún reembolso (facturas rectificativas de proveedor)

- Nombre de la empresa
- Número de factura
- Fecha de la factura
- Total factura SIN impuestos
  
Ordenadas por fecha de factura de modo que la primera sea la más reciente.

(Utilice distinct para eliminar duplicados)

![imagen](https://github.com/user-attachments/assets/945262c1-f378-45b1-a687-5488d40b66b8)

SELECT Distinct invoice_partner_display_name, invoice_date, amount_untaxed
	FROM account_move
	where move_type='in_refund'

Apartado 6

Utilizando las tablas de odoo, obtén un listado de empresas clientes, a las que se les
ha emitido más de dos facturas de venta (solo venta) confirmadas, mostrando los
siguientes datos:

- Nombre de la empresa
- Número de facturas 
- Total facturado SIN IMPUESTOS

![imagen](https://github.com/user-attachments/assets/14d1c1b6-0556-4ee1-be4d-a77c1768d53e)

SELECT invoice_partner_display_name, Count(Distinct name) As Numero_de_facturas, Sum(Distinct amount_untaxed) As Total_facturado from account_move
Where move_type='out_invoice' AND state='posted'
Group by invoice_partner_display_name
Having Count(Distinct name)>2

Apartado 7

Crea una sentencia que actualice el correo de los contactos cuyo dominio es
@bilbao.example.com a @bilbao.bizkaia.eus

![imagen](https://github.com/user-attachments/assets/4ebc4913-25f8-4d66-a456-b87feaa7b6ab)

UPDATE res_partner
Set email = Replace(email,'@bilbao.example.com' ,'@bilbao.bizkaia.eus')
Where email Like '%@bilbao.example.com'

Select email from res_partner
WHERE email LIKE '%@bilbao.bizkaia.eus';

Apartado 8

La empresa Ready Mat ha hecho un ERE y ha despedido a todos los empleados
que tenías como contacto. Crea una sentencia que elimine todos los contactos
pertenecientes a la empresa “Ready Mat”, pero mantén la empresa. Añade una
captura de pantalla de la sección de contactos de odoo con Ready Mat antes y
después

Antes del borrado.

![imagen](https://github.com/user-attachments/assets/ecfe347e-86d7-4906-a29e-7aa69bac898d)

![imagen](https://github.com/user-attachments/assets/7a70e250-d419-4765-a619-d018b625d12b)

Delete from res_partner
where commercial_company_name = 'Ready Mat' AND is_company = false

Despues del borrado



