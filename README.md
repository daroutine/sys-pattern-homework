# Домашнее задание к занятию "SQL. Часть 2" - `Зарецкий Ю.М.`




### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.

### Ответ:
![1](https://github.com/daroutine/sys-pattern-homework/blob/main/1.jpg);

'select concat(sotr.first_name , ' ', sotr.last_name) as Сотрудник,  c2.city as Город, COUNT(c.customer_id) as "Покупатели"
from staff sotr
join store s2 on s2.store_id = sotr.store_id 
join customer c on c.store_id = s2.store_id
join address a on a.address_id = s2.address_id 
join city c2 on c2.city_id = a.city_id 
group by sotr.staff_id, c2.city_id 
having COUNT(c.customer_id) > 300;'

### Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Ответ:
![2](https://github.com/daroutine/sys-pattern-homework/blob/main/2.jpg);

'select count(film_id) as "количество фильмов" from film 
where length > (select AVG(length) from film);'
### Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Ответ:

![3](https://github.com/daroutine/sys-pattern-homework/blob/main/3.png);

'select month(payment_date) as Месяц, SUM(p.amount) "Сумма платежей", COUNT(p.rental_id) "Количество аренд" 
from payment p
group by MONTH(payment_date)
order by SUM(p.amount ) 
desc limit 1;'
