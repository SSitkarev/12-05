# Домашнее задание к занятию 12-05 «Индексы» - Сергей Ситкарёв

## Задание 1

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

![Задание1](https://github.com/SSitkarev/12-05/blob/main/img/1.jpg)

## Задание 2

Выполните explain analyze следующего запроса:

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id

перечислите узкие места;

оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.

### Ответ:

Проанализировав запрос, можно сделать вывод, что его целью является вывод сумм платежей по клиетам за дату 2005-07-30. 
Вся необходимая информация для этого содержится в таблицах payment и customer.
В исправленном запросе будем основываться на данных из этих таблиц:

![Задание2](https://github.com/SSitkarev/12-05/blob/main/img/2.jpg)

Видим, что запрос теперь обрабатывается 0,015, вместо 4,391 секунд.
