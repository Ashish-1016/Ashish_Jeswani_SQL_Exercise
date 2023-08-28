-- 1. return movie name, customer name for all payments above 5.
-- 2. return actor full name, film name for all films having rental rate greater than 2.5.
-- 3. return film name which is most times rented out.
-- 4. return customer name who rented out movie more than 20 times.
-- 5. return total money earned from movie id 2

--Ans1:
SELECT f.title, c.first_name
FROM payment p
         JOIN customer c ON p.customer_id = c.customer_id
         JOIN rental r ON p.rental_id = r.rental_id
         JOIN inventory i ON r.inventory_id = i.inventory_id
         JOIN film f ON i.film_id = f.film_id
WHERE p.amount > 5;

--Ans2:
SELECT a.first_name || ' ' || a.last_name as actor_name, f.title
FROM film f
        JOIN film_actor fa USING (film_id)
        JOIN actor a USING (actor_id)
WHERE f.rental_rate > 2.5;

--Ans3:
SELECT f.title
FROM film f
         JOIN inventory i USING (film_id)
         JOIN rental r USING (inventory_id)
GROUP BY f.title
ORDER BY count(r.rental_id) DESC
LIMIT 1;

--Ans4:
SELECT c.first_name
FROM customer c
        JOIN rental r USING (customer_id)
GROUP BY c.first_name,c.customer_id
HAVING count(r.rental_id) >20;

--Ans5:
SELECT sum(p.amount) AS movie_revenue
FROM payment p
         JOIN rental r USING (rental_id)
         JOIN inventory i USING (inventory_id)
WHERE i.film_id = 2;
