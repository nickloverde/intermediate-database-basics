-- SELECT \*
-- FROM invoice i
-- JOIN invoice_line il ON il.invoice_id = i.invoice_id
-- WHERE il.unit_price > 0.99;

-- SELECT i.invoice_date, c.first_name, c.last_name, i.total
-- FROM invoice i
-- JOIN customer c ON i.customer_id = c.customer_id;

-- SELECT c.first_name, c.last_name, e.first_name, e.last_name
-- FROM customer c
-- JOIN employee e ON c.support_rep_id = e.employee_id;

-- SELECT al.title, ar.name
-- FROM album al
-- JOIN artist ar ON al.artist_id = ar.artist_id;

-- SELECT pt.track_id
-- FROM playlist_track pt
-- JOIN playlist p ON p.playlist_id = pt.playlist_id
-- WHERE p.name = 'Music';

-- SELECT t.name
-- FROM track t
-- JOIN playlist_track pt ON pt.track_id = t.track_id
-- WHERE pt.playlist_id = 5;

-- SELECT t.name, p.name
-- FROM track t
-- JOIN playlist_track pt ON pt.track_id = t.track_id
-- JOIN playlist p ON pt.playlist_id = p.playlist_id;

-- SELECT t.name, al.title
-- FROM track t
-- JOIN album al ON t.album_id = al.album_id
-- JOIN genre g ON g.genre_id = t.genre_id
-- WHERE g.name = 'Alternative & Punk';

-- SELECT t.name AS track_name, g.name AS genre, al.title AS album_title, ar.name AS artist
-- FROM track t
-- JOIN

-- Nested Queries

-- SELECT \*
-- FROM invoice
-- WHERE invoice_id IN
-- (SELECT invoice_id
-- FROM invoice_line
-- WHERE unit_price > 0.99);

-- SELECT \*
-- FROM playlist_track
-- WHERE playlist_id IN
-- (SELECT playlist_id
-- FROM playlist
-- WHERE name = 'Music');

-- SELECT name
-- FROM track
-- WHERE track_id IN
-- (SELECT track_id
-- FROM playlist_track
-- WHERE playlist_id = 5);

-- SELECT \*
-- FROM track
-- WHERE genre_id IN
-- (SELECT genre_id
-- FROM genre
-- WHERE name = 'Comedy');

-- SELECT \*
-- FROM track
-- WHERE album_id IN (
-- SELECT album_id
-- FROM album
-- WHERE artist_id IN (
-- SELECT artist_id
-- FROM artist
-- WHERE name = 'Queen'));

-- Practice Updating Rows

-- UPDATE customer
-- SET fax = null
-- WHERE fax IS NOT null;

-- UPDATE customer
-- SET company = 'Self'
-- WHERE company IS null;

-- SELECT \* FROM customer
-- WHERE company ='Self';

-- UPDATE customer
-- SET last_name = 'Thompson'
-- WHERE first_name = 'Julia' AND last_name = 'Barnett';

-- SELECT \* FROM customer
-- WHERE last_name = 'Thompson';

-- UPDATE customer
-- SET support_rep_id = 4
-- WHERE email = 'luisrojas@yahoo.cl';

-- SELECT support_rep_id FROM customer
-- WHERE email = 'luisrojas@yahoo.cl';

UPDATE track
SET composer = 'The darkness around us'
WHERE genre_id =
(SELECT genre_id
FROM genre
WHERE name = 'Metal')
AND composer IS null;

-- Group By

-- SELECT COUNT(\*), g.name
-- FROM track t
-- JOIN genre g ON t.genre_id = g.genre_id
-- GROUP BY g.name;

-- SELECT COUNT(\*)
-- FROM track t
-- JOIN genre g ON g.genre_id = t.genre_id
-- WHERE g.name = 'Pop' OR g.name = 'Rock'
-- GROUP BY g.name;

-- SELECT COUNT(\*), ar.name
-- FROM album al
-- JOIN artist ar ON ar.artist_id = al.artist_id
-- GROUP BY ar.name;

-- Distinct

-- SELECT DISTINCT composer
-- FROM track;

-- SELECT DISTINCT billing_postal_code
-- FROM invoice;

-- SELECT company
-- FROM customer;

-- Delete Rows

-- CREATE TABLE practice_delete ( name TEXT, type TEXT, value INTEGER );
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'bronze', 50);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'bronze', 50);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'bronze', 50);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'silver', 100);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'silver', 100);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);
-- INSERT INTO practice_delete ( name, type, value ) VALUES ('delete', 'gold', 150);

-- SELECT \* FROM practice_delete;

-- DELETE FROM practice_delete
-- WHERE type= 'bronze';

-- DELETE FROM practice_delete
-- WHERE type='silver';

-- DELETE FROM practice_delete
-- WHERE value = 150;

-- -DevMountain schema crashed and I lost what I had previously written

-- eCommerce

-- CREATE TABLE users (
-- user_id SERIAL PRIMARY KEY,
-- name VARCHAR(250),
-- email VARCHAR(250)
-- );

-- CREATE TABLE product (
-- product_id SERIAL PRIMARY KEY,
-- product_name VARCHAR(250),
-- price NUMERIC
-- );

-- CREATE TABLE orders (
-- order_id SERIAL PRIMARY KEY,
-- product_id INT REFERENCES product(product_id)
-- );

-- INSERT INTO users (name, email)
-- VALUES ('Jacob', 'jacob@gmail.com'),
-- ('Jasper', 'jasper@gmail.com'),
-- ('Jeffrey', 'jeffrey@gmail.com');

-- SELECT \* FROM users;

-- INSERT INTO product (product_name, price)
-- VALUES ('kidney beans', 0.99),
-- ('lima beans', 1.99),
-- ('pinto beans', 2.99)
-- ;

-- SELECT \* FROM product;

-- INSERT INTO orders (product_id)
-- VALUES (2,1), (1,2), (3,3);

SELECT \* FROM orders o
JOIN product p ON p.id = o.product_id
WHERE o.id = 1

ALTER TABLE orders
ADD COLUMN user_id INT REFERENCES user(id)

SELECT count(\*)
FROM orders 0
JOIN product p on p.id = o.product_id
JOIN users u ON u.id = o.user_id
GROUP BY u.id
