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


Apartado 2

Inserta 5 registros inventados en la tabla a través de una sentencia SQL.

![imagen](https://github.com/user-attachments/assets/b27a68d2-bb7d-42ca-af04-4d84a32186cf)


Apartado 3

Realiza una consulta donde se muestren todos los datos de la tabla EmpresasFCT
ordenados por fechaContacto, de modo que en la primera fila salga el que tenga la
fecha más reciente.

![imagen](https://github.com/user-attachments/assets/c2774b2f-ebae-44bf-99d1-8c406e37da91)


Apartado 4

Realiza una consulta que permita obtener un listado de todos los contactos de
Odoo (no empresas) con la siguiente información:

- Nombre
- Cuya ciudad sea Tracy
- Nombre comercial de la empresa
  
Ordenados alfabéticamente por el nombre comercial de la empresa.

![imagen](https://github.com/user-attachments/assets/9ac7ee19-2302-45e0-90f6-98eeb4161dbb)


Apartado 5

Utilizando las tablas de odoo, obtén un listado de empresas proveedoras, que han
emitido algún reembolso (facturas rectificativas de proveedor)

- Nombre de la empresa
- Número de factura
- Fecha de la factura -total de factura con impuestos
- Total factura SIN impuestos
  
Ordenadas por fecha de factura de modo que la primera sea la más reciente.

Apartado 6

Utilizando las tablas de odoo, obtén un listado de empresas clientes, a las que se les
ha emitido más de dos facturas de venta (solo venta) confirmadas, mostrando los
siguientes datos:

- Nombre de la empresa
- Número de facturas -total de factura con impuestos
- Total facturado SIN IMPUESTOS

Apartado 7

Crea una sentencia que actualice el correo de los contactos cuyo dominio es
@bilbao.example.com a @bilbao.bizkaia.neus

Apartado 8

La empresa Ready Mat ha hecho un ERE y ha despedido a todos los empleados
que tenías como contacto. Crea una sentencia que elimine todos los contactos
pertenecientes a la empresa “Ready Mat”, pero mantén la empresa. Añade una
captura de pantalla de la sección de contactos de odoo con Ready Mat antes y
después
