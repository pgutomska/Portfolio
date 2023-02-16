#### 1. Wyświetl tabelę actors w kolejności alfabetycznej sortując po kolumnie surname.

SELECT * FROM actors

ORDER BY surname

![z01](https://user-images.githubusercontent.com/122393705/218308196-81f72d00-ad0f-49af-a451-57434152f7fb.png)

#### 2. Wyświetl film, który powstał w 2019 roku

SELECT * FROM movies

WHERE year_of_production = 2019

![z02](https://user-images.githubusercontent.com/122393705/218308211-4c01d970-3cdd-4f4f-8e04-b1e334061b40.png)

#### 3. Wyświetl wszystkie filmy, które powstały między 1900, a 1999 rokiem.

SELECT * FROM movies

WHERE year_of_production BETWEEN 1900 AND 1999

![z03](https://user-images.githubusercontent.com/122393705/218308221-bb3a0983-6280-4348-b6ab-de79e0f624da.png)

#### 4. Wyświetl JEDYNIE tytuł i cenę filmów, które kosztują poniżej 7$

SELECT title, price

FROM movies

WHERE price < 7

![z04](https://user-images.githubusercontent.com/122393705/218308226-559033a5-6f06-4fc5-9d2c-7b011fe44c3b.png)

#### 5. Użyj operatora logicznego AND, aby wyświetlić aktorów o actor_id pomiędzy 4-7 (4 i 7 powinny się wyświetlać). NIE UŻYWAJ operatora BETWEEN.

SELECT * FROM actors

WHERE actor_id >=  4 AND actor_id <= 7

ORDER BY actor_id

![z05](https://user-images.githubusercontent.com/122393705/218308231-e96f861c-9015-46fc-ba92-08dd695db20e.png)

#### 6. Wyświetl klientów o id 2,4,6 wykorzystaj do tego warunek logiczny.

SELECT * FROM customers

WHERE customer_id =2 OR customer_id = 4 OR customer_id = 6

ORDER BY customer_id

![z06](https://user-images.githubusercontent.com/122393705/218308235-a8d7abf6-1f92-4819-aa43-31c44c13fda2.png)

#### 7. Wyświetl klientów o id 1,3,5 wykorzystaj do tego operator IN.

SELECT * FROM customers

WHERE customer_id IN (1,3,5)

![z07](https://user-images.githubusercontent.com/122393705/218308237-44074615-4c0f-4865-8f36-4871ea08be6b.png)

#### 8. Wyświetl dane wszystkich osób z tabeli 'actors', których imię zaczyna się od ciągu "An".

SELECT * FROM actors 

WHERE name LIKE 'An%'

ORDER BY name

![z08](https://user-images.githubusercontent.com/122393705/218308243-a01267b1-ebf0-43f4-9e72-ddc808eb472e.png)

#### 9. Wyświetl dane klienta, który nie ma podanego adresu email.

SELECT * FROM customers

WHERE email IS NULL

![z09](https://user-images.githubusercontent.com/122393705/218308251-97269814-bb27-460d-b125-941d4eec103f.png)

#### 10. Wyświetl wszystkie filmy, których cena wynosi powyżej 9$ oraz ich ID mieści się pomiędzy 2 i 8 movie_id.

SELECT * FROM movies

WHERE price > 9 AND movie_id >= 2 AND movie_id <= 8

![z10](https://user-images.githubusercontent.com/122393705/218308254-39f55910-4e38-4b0d-b4a3-6a91e8e0f665.png)

#### 11.  Popełniłam błąd wpisując nazwisko Ani Miler – wpisałam Muler. Znajdź i zastosuj funkcję, która poprawi mój karkołomny błąd 

UPDATE customers

SET  surname = 'Miler'

WHERE customer_id = 3

![z11](https://user-images.githubusercontent.com/122393705/219426178-b59cdcd1-e689-4bdd-bcb7-9480a4900ea0.png)

#### 12. Pobrałam za dużo pieniędzy od klienta, który kupił w ostatnim czasie film o id 4. Korzystając z funkcji join sprawdź, jak ma na imię klient 
i jakiego ma maila. W celu napisania mu wiadomości o pomyłce fantastycznej szefowej.

SELECT * FROM customers

JOIN sale

ON customers.customer_id = sale.customer_id

WHERE movie_id = 4

ORDER BY sale_date DESC

LIMIT 1

![z12](https://user-images.githubusercontent.com/122393705/219426245-71cbc843-ebdb-4a99-aec5-b1f87667c256.png)

#### 13. Na pewno zauważył_ś, że sprzedawca zapomniał wpisać emaila klientce Patrycji. Uzupełnij ten brak wpisując: pati@mail.com

UPDATE customers

SET email = 'pati@mail.com'

WHERE customer_id = 4

![z13](https://user-images.githubusercontent.com/122393705/219426273-b849ec8e-6879-4dcc-a15f-bb99354e82b1.png)

#### 14. Dla każdego zakupu wyświetl, imię i nazwisko klienta, który dokonał wypożyczenia oraz tytuł wypożyczonego filmu. (wykorzystaj do tego funkcję inner join, zastanów się wcześniej, które tabele Ci się przydadzą do wykonania ćwiczenia).

SELECT c.name, c.surname, m.title

FROM customers AS c 

INNER JOIN sale AS s

ON c.customer_id = s.customer_id

INNER JOIN movies AS m

ON s.movie_id = m.movie_id

![z14](https://user-images.githubusercontent.com/122393705/219426305-49ceb5fe-5ff0-4a2d-8293-8bb025fa2200.png)

#### 15. W celu anonimizacji danych, chcesz stworzyć pseudonimy swoich klientów. - Dodaj kolumnę o nazwie ‘pseudonym’ do tabeli customers,- Wypełnij kolumnę w taki sposób, aby pseudonim stworzył się z dwóch pierwszych liter imienia i ostatniej litery nazwiska. Np. Natalie Pilling → Nag

ALTER TABLE customers

ADD pseudonym nvarchar(3);

UPDATE customers

SET pseudonym = CONCAT(LEFT(name, 2), RIGHT(surname, 1))

![z15](https://user-images.githubusercontent.com/122393705/219426328-1abd790b-c87a-4d42-9e31-9fb95d7fcc5d.png)

#### 16. Wyświetl tytuły filmów, które zostały zakupione, wyświetl tabelę w taki sposób, aby tytuły się nie powtarzały.

SELECT DISTINCT title FROM movies

JOIN sale

![z16](https://user-images.githubusercontent.com/122393705/219426349-5b1abfeb-c1fc-41b4-a59d-3403c6810fae.png)

#### 17. Wyświetl wspólną listę imion wszystkich aktorów i klientów, a wynik uporządkuj alfabetycznie. (Wykorzystaj do tego funkcji UNION)

SELECT name FROM actors

UNION 

SELECT name FROM customers

ORDER BY name

![z17](https://user-images.githubusercontent.com/122393705/219426378-665c853b-a5e0-4a90-ad35-e6b89855b5df.png)

#### 18. Polskę opanowała inflacja i nasz sklepik z filmami również dotknął ten problem. Podnieś cenę wszystkich filmów wyprodukowanych po 2000 roku o 2,5 $ (Pamiętaj, że dolar to domyślna jednostka- nie używaj jej nigdzie).

UPDATE movies

SET price = price+2.5

WHERE year_of_production > 2000

![z18](https://user-images.githubusercontent.com/122393705/219426405-9817c0e9-e37d-4a48-a93a-98fa68fb8143.png)

#### 19. Wyświetl imię i nazwisko aktora o id 4 i tytuł filmu, w którym zagrał

SELECT a.name, a.surname, m.title 

FROM actors AS a

JOIN cast AS c

ON a.actor_id = c.actor_id

JOIN  movies AS m

ON m.movie_id = c.movie_id

WHERE a.actor_id = 4

![z19](https://user-images.githubusercontent.com/122393705/219426420-ce4934e6-ed03-4bfe-b2b8-f5b95fdd09c3.png)

#### 20. A gdzie nasza HONIA!? Dodaj do tabeli customers nową krotkę, gdzie customer_id = 7, name = Honia, surname = Stuczka-Kucharska, email = honia@mail.com oraz pseudonym = Hoa

INSERT INTO customers VALUES (7, 'Honia', 'Stuczka-Kucharska', 'honia@mail.com', 'Hoa'

![z20](https://user-images.githubusercontent.com/122393705/219426441-8e5b3ff4-440f-4bf2-8dae-47d25ebdf33d.png)
