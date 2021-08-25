# MYSQL
SAKILA
1. select * from actor;
2. SELECT last_name FROM actor WHERE first_name='John';
3. select * from actor where last_name='Neeson';
4. select * from actor where actor_id%10=0;
5. select description from film where film_id=100;
6. select * from film where rating='R';
7. select * from film where rating!='R';
8. select * from film ORDER BY length ASC LIMIT 10;
9. SELECT title AS "Film title", length as "Runtime (minutes)"FROM film
WHERE length = (
    SELECT Max(length)
    FROM film
    )
ORDER BY title ASC;

10. SELECT * FROM film WHERE special_features LIKE "%Deleted Scenes%";

11. SELECT last_name,COUNT(*) FROM actor GROUP BY last_name HAVING COUNT(*)=1 ORDER BY last_name DESC;

12. SELECT last_name,COUNT(*) FROM actor GROUP BY last_name HAVING COUNT(*)>1 ORDER BY COUNT(*) DESC;

13. select actor.first_name,actor.last_name,count(film_actor.film_id) as movies from actor
join
film_actor
on
actor.actor_id=film_actor.actor_id
group by actor.actor_id order by movies desc limit 1;

14. SELECT release_year FROM film WHERE title='Academy Dinosaur';

15. SELECT AVG(length) FROM film;

16. select film_category.category_id,AVG(film.length) from film
join film_category
on
film.film_id=film_category.film_id
group by film_category.category_id order by film_category.category_id asc ;

17. select * from film where description like '%robot%';

18. select release_year,COUNT(film_id) from film where release_year='2010' group by release_year;

19. select film.title from film
join genres_movies
on genres_movies.movie_id=film.film_id
where genres_movies.genre_id=11;

20. select first_name,last_name from staff where staff_id=2;

21. select film.title from film
join film_actor
on film.film_id =film_actor.film_id
where film_actor.actor_id=16;

22. SELECT COUNT(DISTINCT country) AS "Number of countries" from country;

23. select name from language order by name desc;

24. select first_name,last_name from actor where last_name like '%son' order by first_name asc;

25. SELECT category AS "Category", COUNT(category) AS "Number of films" FROM film_list GROUP BY category ORDER BY COUNT(category) DESC LIMIT 1;


WORLD
1. select count(name) from city where CountryCode='USA';
2. select Population,LifeExpectancy from country where name='Argentina';
3. select name,LifeExpectancy from country where LifeExpectancy is not null order by LifeExpectancy desc limit 1;
4. select city.Name from city join country on city.ID = country.Capital where country.Name='Spain';
5. select countryLanguage.Language from countryLanguage join country on countryLanguage.CountryCode=country.Code where Region='Southeast Asia';
6. select Name from city where Name like 'F%' limit 25;
7. select country.Name,COUNT(city.ID) from country join city on country.Code=city.CountryCode where city.CountryCode='CHN';
8. select Name,Population from country where Population is not null order by Population desc limit 1;

9. select COUNT(Name) from country;

10. select Name,SurfaceArea from country order by SurfaceArea desc limit 10;
11. select Name,Population from city where CountryCode = 'JPN' order by Population desc limit 5;
12. UPDATE `country`
 SET `HeadOfState` = replace(HeadOfState, 'Elisabeth II', 'Elizabeth II')

select Code,Name from country where HeadOfState='Elizabeth II';

13. select Name from country where Population/SurfaceArea >0 order by Population/SurfaceArea asc limit 10;

14. select distinct Language from countrylanguage;

15. select Name,GNP from country order by GNP desc limit 10;

16. select country.Name,COUNT(countrylanguage.Language) as NoOfLAng from country join countrylanguage on country.Code = countrylanguage.CountryCode group by country.Name order by NoOfLAng desc limit 10;

17. select Language,CountryCode from countrylanguage where Language='German' AND Percentage>50.0;

18. select Name,LifeExpectancy from country where LifeExpectancy is not null order by LifeExpectancy asc limit 1;

19. select GovernmentForm,COUNT(GovernmentForm) as Forms from country group by GovernmentForm order by Forms desc limit 3;

20.select count(IndepYear) from country where IndepYear is not null;

MOVIELENS

1. select title from movies where release_date between '1983-01-01' AND '1993-12-31' order by release_date desc ;

2. select movies.title from movies join ratings on movies.id=ratings.movie_id where ratings.rating =1;

3. select distinct * from movies where id in (
select movie_id from ratings where user_id in (select id from users where occupation_id=19 and age=24) AND rating=5) AND id in (select movie_id from genres_movies where genre_id=15);

4. select title from movies where release_date=(select release_date from movies group by release_date order by COUNT(release_date) desc limit 1);

5. select genre_id,COUNT(movie_id) as total from genres_movies group by genre_id order by total asc;
