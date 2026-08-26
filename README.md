¿Por qué usaste LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué se perdería si usaras INNER JOIN?
Use Left join porque es necesario mostrar todos los productos, incluso los que no tienen ventas, y con INNER JOIN  se perderian esos productos sin coincidencias en ventas. 

¿Por qué usaste RIGHT JOIN para la Consulta 2? ¿Qué tabla está a la izquierda y cuál a la derecha en tu consulta?
Use RIGHT JOIN porque la consulta busca identificar si existen ventas registradas cuyo productos no figuran en el catálogo. En mi consulta la tabla Productos está a la izquierda y la tabla ventas esta a la derecha.  El RIGHT JOIN permite conservar todas las ventas, incluso aquellas que no tienen un producto correspondiente en la tabla Productos. En esos casos, las columnas de producto aparecen como NULL. 

¿Qué representan los valores NULL en cada resultado? Explicá con un ejemplo concreto de los datos qué significa que venta_id sea NULL en la Consulta 1 y que producto_id de productos sea NULL en la Consulta 2.
En la consulta 1 los valores NULL representan los productos que nunca han sido vendidos, se identifican como HUB USB-C 7p y Parlante Bluetooth y aparecen igual en la tabla, pero con NULL en ventas. 
En la consulta 2 el valor NULL representa que se realizo una venta que no esta asociada a ningun producto correspondiente a la tabla de productos, por lo tanto es probable que se trate de un error. 
¿Cuándo usarías FULL OUTER JOIN en un caso real de negocio?
Usarias FULL OUTER JOIN para conciliar registros de ventas, por ejemplo si necesitaria corroborar que todos los tickets de ventas esten asociados a un medio de pago. 
