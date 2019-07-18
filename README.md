
# Prueba para soporte técnico Luuna

## SQL Básico

Existen 3 tablas de SQL con la siguiente información:

-**1. Order**: es una tabla con la información básica de la orden. La orden con id 567 contiene la siguiente información:

| id  | order_number  | order_total  | user_email  | user_id  | created_at |
|---|---|---|---|---|---|
|  ... | ... | ... | ... | ...  | ...  |
|  567 | 19857758784 | 29000 | alvaro.burgos | 5  | 2019-06-10 13:45:00  |
|  ... | ... | ... | ... | ...  | ...  |

-**2. OrderItem**: Contiene información básica de los items asociados a esa orden. La orden con id 567 contiene 3 items: el 56 , 57 y 58.

| id  | order_id  | sku  | price  | discount  | created_at |
|---|---|---|---|---|---|
|  ... | ... | ... | ... | ...  | ...  |
|  56 | 567 | LU1001 | 20000 | 0  | 2019-06-10 13:45:00  |
|  57 | 567 | LU1002 | 4500 | 0  | 2019-06-10 13:45:00  |
|  58 | 567 | LU1002 | 4500 | 0  | 2019-06-10 13:45:00  |
|  ... | ... | ... | ... | ...  | ...  |

-**3. MachineItem**: Mantiene el estado actual en que se ecuentra el item al igual que su historial. La columna `is_active` detona el estado actual si es igual a 1, y los estados historicos se identifican con el valor igual a 0.

Ejemplo: El item `56` estuvo en el estado `shipping_pending` en la fecha `2019-06-10 13:45:00`. Posteriormente en la fecha `2019-06-10 15:45:00` cambió al estado `shipping_approved`, que es en estos momentos el estado actual en el que se ecuentra el item. El item `57` y `58` estan en `shipping_pending` y nunca estuvieron en niguno otro estado.

| id  | order_id  | item_id  | is_active  | status  | created_at |
|---|---|---|---|---|---|
|...|...|...|...|...|...|
|  23 | 567 | 56 | 0 | shipping_pending  | 2019-06-10 13:45:00  |
|  24 | 567 | 57 | 1 | shipping_pending  | 2019-06-10 13:45:00  |
|  25 | 567 | 58 | 1 | shipping_pending  | 2019-06-10 13:45:00  |
|  26 | 567 | 56 | 1 | shipping_approved | 2019-06-10 15:45:00  |
|...|...|...|...|...|...|

### Contesta a lo siguiente:

1. Utilizando una sola query: Alguién quiere saber cuales son los `sku` de la orden con `order_number` igual a `19857758784` que se encuentran en el `status` actual de `shipping_pending`.
select Order.order_number,OrderItem.sku,MachineItem.status
from order
Inner Join OrderItem, MachineItem
On Order.order_number=OrderItem.sku And Order.order_number= MachineItem.statud;
Where order_number=19857758784 Ando status=shipping_pending

2. Utilizando 2 queries: Alguién quiere pasar los items que se encuentran actualmente en el estado `shipping_pending` de la  `order_number` igual a `19857758784` al status `shipping_approved`.
Update MachineItem ser status=shipping_approved
Where status=shipping_pending  ADN order_number=19857758784

IMPORTANTE: En ambos casos no sabes los valores para item_id o order_id solo que el `order_number` de la orden es igual a `19857758784`


