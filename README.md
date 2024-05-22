# Домашнее задание к занятию "`SQL. Часть 2`" - `Тен Денис`


### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение Задание 1

```sql
SELECT s.first_name, s.last_name, c.city, COUNT(cst.customer_id) AS customer_count
FROM staff AS s
INNER JOIN store AS st ON s.store_id = st.store_id
INNER JOIN address AS a ON st.address_id = a.address_id
INNER JOIN city AS c ON a.city_id = c.city_id
INNER JOIN customer AS cst ON cst.store_id = st.store_id
GROUP BY s.first_name, s.last_name, c.city
HAVING COUNT(cst.customer_id) > 300;
```
![image](https://github.com/killakazzak/12-04-sdb-hw/assets/32342205/a4a1bb1d-3afa-4030-a15b-b96e062a85b3)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение Задание 2

```sql
SELECT COUNT(*) AS film_count
FROM film
WHERE length > (
    SELECT AVG(length)
    FROM film
);
```
![image](https://github.com/killakazzak/12-04-sdb-hw/assets/32342205/a9ce1449-3bcc-44fd-a989-a62520fa60de)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение Задание 3

```sql
SELECT MONTH(payment_date) AS month, SUM(amount) AS total_payment, COUNT(rental_id) AS rental_count
FROM payment
GROUP BY MONTH(payment_date)
ORDER BY total_payment DESC
LIMIT 1;
```
![image](https://github.com/killakazzak/12-04-sdb-hw/assets/32342205/3e99131a-0069-411a-8508-6909dc1acd7e)


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Решение Задание 4*

```sql
SELECT staff_id, COUNT(rental_id) AS total_sales,
    CASE
        WHEN COUNT(rental_id) > 8000 THEN 'Да'
        ELSE 'Нет'
    END AS Премия
FROM rental
GROUP BY staff_id;
```
![image](https://github.com/killakazzak/12-04-sdb-hw/assets/32342205/75844d2e-bbe6-467d-a229-d2529fee6180)

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.

### Решение Задание 5*







