# Advanced SELECT

## Setup

You should have already created a Google Cloud account, created an instance and built a database (yesterday), as well as installed MySQL Workbench and made a connection to the database you've created.. In this lesson we will practice querying data.

* Open MySQL Workbench

## Part 1 - Initialize data

We'll use the same database as we did yesterday but this new initialization will delete or `DROP` our existing table of `users` and replace it with three new tables: `usersAddress`, `users`, & `usersContact`. To do this:

* Make sure you've selected the "admin" database in MySQL Workbench

* Create a new query tab
  * Click the button on the top left that has a SQL file with a "plus" icon on it

* Click the folder icon in your query tab to open a new file

* Select the "initialize.sql" script that lives in this repo (you've hopefully cloned it into your 311-JSDev folder or somewhere else)

* Click the lightning bolt icon to run the query

* If you refresh your schemas you should see a "users", "usersContact" and "usersAddress" table

## Part 2 - Query data

We are going to run a couple SQL queries and put the answers in the "Query Responses" section of this README. The query instructions are intentionally written in plain english. It's up to you to translate that into a SELECT statement.

1. Get a sum of all the user_ids from the `usersAddress` table grouped by state. Enter the values for the specific states below.
```
SELECT
	state,
    sum(user_id) as sums
FROM
    usersAddress
GROUP BY state
order by state
```

```
SELECT
	state,
    counts(user_id) as counts
FROM
    usersAddress
GROUP BY state
order by state
```

2. Find the most popular area code in the `usersContact` table. 
  * Hint: SUBSTR, GROUP BY
```
SELECT
	substr(phone1, 1, 3) as phone1,
  count(*) as phoneCount
FROM
  usersContact
GROUP BY substr(phone1, 1, 3)
ORDER BY phoneCount desc
```

3. Find the MIN first_name, the county, and a count of all users in that county for counties with more than 10 users. There will be four results. List the last one. 
  * Hint: MIN, COUNT, JOIN, GROUP BY, HAVING
```
SELECT
	MIN(first_name),
  county,
  count(user_id) as idCount
FROM 
	users LEFT OUTER JOIN usersAddress USING(id)
GROUP BY county
	HAVING idCount > 10
ORDER BY idCount desc
```

## Query Responses

1. Sums
  * AK: 6 (Count) / 1422 (Sum)
  * CT: 5 (Count) / 999 (Sum)
  * TX: 32 (Count) / 7908 (Sum)
  * WY: 3 (Count) / 1271 (Sum)

2.
  * Area code: (973) Count: 18

3.
  * first_name: Avery
  * county: Orange
  * county total: 11


## Summary

We're starting to get pretty advanced with our SQL queries. Keep researching other advanced SELECT statements and get ready to foray into [INSERTs and UPDATEs and DELETEs, oh CRUD](https://www.youtube.com/watch?v=-HrfbV16-FQ)!.
