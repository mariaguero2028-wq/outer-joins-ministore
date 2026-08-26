Por qué usaste LEFT JOIN para la Consulta 1 y no INNER JOIN? ¿Qué se perdería si usaras INNER JOIN?

Usé LEFT JOIN porque es necesario mostrar todos los productos del catálogo, incluso los que no tienen ventas asociadas. La tabla productos es la tabla de la izquierda, por lo que el LEFT JOIN permite conservar todos sus registros, aunque no exista una coincidencia en la tabla ventas.

En este ejercicio, los productos con producto_id 108, Hub USB-C 7p, y 109, Parlante Bluetooth, nunca fueron vendidos. Por eso aparecen en el resultado con NULL en las columnas correspondientes a las ventas.

Si utilizara INNER JOIN, solamente se mostrarían los productos que tienen al menos una venta asociada. En consecuencia, los productos 108 y 109 se perderían y no podríamos identificar que existen productos en el catálogo que nunca fueron vendidos.

El filtro WHERE v.venta_id IS NULL permite mostrar únicamente los productos que no tienen ventas.

¿Por qué usaste RIGHT JOIN para la Consulta 2? ¿Qué tabla está a la izquierda y cuál a la derecha en tu consulta?

Usé RIGHT JOIN porque la consulta busca identificar si existen ventas registradas cuyos productos no figuran en el catálogo.

En mi consulta, la tabla productos está a la izquierda y la tabla ventas está a la derecha:

FROM productos p
RIGHT JOIN ventas v
    ON p.producto_id = v.producto_id

El RIGHT JOIN permite conservar todas las ventas, incluso aquellas que no tienen un producto correspondiente en la tabla productos. Cuando no existe coincidencia, las columnas provenientes de productos aparecen como NULL.

En este ejercicio, la venta con venta_id = 10 tiene asociado el producto_id = 999, pero ese producto no existe en el catálogo. Por lo tanto, esta venta es identificada como un registro huérfano.

El filtro WHERE p.producto_id IS NULL permite aislar específicamente este caso.

¿Qué representan los valores NULL en cada resultado?

Los valores NULL representan que no existe una coincidencia entre las tablas relacionadas.

En la Consulta 1, cuando venta_id aparece como NULL, significa que el producto existe en el catálogo pero no tiene ninguna venta asociada. Por ejemplo, el Hub USB-C 7p (producto 108) y el Parlante Bluetooth (producto 109) aparecen en la tabla de productos, pero nunca fueron vendidos. Por eso sus datos de venta aparecen como NULL.

En la Consulta 2 ocurre lo contrario. Cuando producto_id de la tabla productos aparece como NULL, significa que existe una venta cuyo producto no se encuentra en el catálogo.

Un ejemplo concreto es la venta 10, que tiene producto_id = 999. Como no existe un producto con ese ID en la tabla productos, los datos correspondientes al producto aparecen como NULL. Esto puede indicar un posible error de carga o inconsistencia en los datos.

Por lo tanto, los valores NULL en estas consultas son útiles para detectar registros que no tienen correspondencia entre las tablas.

¿Cuándo usarías FULL OUTER JOIN en un caso real de negocio?

Usaría FULL OUTER JOIN cuando necesitara comparar o auditar dos conjuntos de datos y quisiera conservar todos los registros de ambas tablas, incluyendo aquellos que no tienen coincidencias.

Por ejemplo, en MiniStore podría utilizarse para realizar una auditoría completa entre el catálogo de productos y las ventas. De esta manera, se pueden identificar al mismo tiempo los productos que existen en el catálogo pero nunca fueron vendidos, como los productos 108 y 109, y las ventas que tienen asociado un producto inexistente, como la venta 10 con producto_id = 999.

En un caso real también podría utilizarse para conciliar información entre dos sistemas, por ejemplo, comparar un listado de ventas de un sistema con otro listado de ventas de un sistema externo. El FULL OUTER JOIN permitiría detectar registros presentes solamente en uno de los dos sistemas, además de aquellos que coinciden en ambos.

Esto resulta útil para procesos de auditoría y control de calidad de datos antes de utilizar la información para generar reportes o dashboards.
