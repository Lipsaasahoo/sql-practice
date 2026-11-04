# SQL Practice !

#### 1. Show first name and last name concatinated into one column to show their full name.

**Solution**

SELECT \
  CONCAT(first_name, '  ', last_name) AS full_name\
FROM patients;

SELECT first_name || ' ' || last_name\
FROM patients;


#### 2. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000

**Solution**

select * from patients where patient_id = 1 or patient_id = 45 or patient_id = 534 or patient_id = 879 or patient_id = 1000

SELECT * \
FROM patients \
WHERE \
  patient_id IN (1, 45, 534, 879, 1000);

#### 3. Show all the columns from admissions where the patient was admitted and discharged on the same day.

**Solution**

SELECT *\
FROM admissions\
WHERE admission_date = discharge_date;

#### 4. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'.

**Solution**

SELECT DISTINCT city AS unique_cities\
FROM patients\
WHERE province_id = 'NS';

SELECT city\
FROM patients\
GROUP BY city\
HAVING province_id = 'NS';

#### 5. Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

**Solution**

select\
	first_name,\
    last_name,\
    birth_date\
from patients\
where height > 160 and weight > 70;

#### 6. Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'

**Solution**

SELECT first_name, last_name, allergies\
FROM patients\
where allergies is not NULL and city = 'Hamilton'.

#### 7. Show unique birth years from patients and order them by ascending.

**Solution**

select distinct year(birth_date)\
from patients\
order by birth_date asc;

#### 8. Show unique first names from the patients table which only occurs once in the list. For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.

**Solution**

SELECT first_name\
FROM patients\
GROUP BY first_name\
HAVING COUNT(first_name) = 1;

SELECT first_name\
FROM (\
    SELECT\
      first_name,\
      count(first_name) AS occurrencies\
    FROM patients\
    GROUP BY first_name\
  )\
WHERE occurrencies = 1

#### 9. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

**Solution**

select patient_id, first_name\
from patients\
where first_name like 's____%s'

#### 10. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

**Solution**

select first_name, last_name, allergies\
from patients\
where allergies = 'Penicillin' or allergies ='Morphine'\
order by allergies asc, first_name asc, last_name asc

SELECT\
  first_name,\
  last_name,\
  allergies\
FROM patients\
WHERE\
  allergies IN ('Penicillin', 'Morphine')\
ORDER BY\
  allergies,\
  first_name,\
  last_name;

#### 11. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

**Solution**

SELECT
  patient_id,
  diagnosis
FROM admissions
GROUP BY
  patient_id,
  diagnosis
HAVING COUNT(*) > 1;

#### 12. Show the city and the total number of patients in the city.Order from most to least patients and then by city name ascending.

**Solution**

SELECT\
  city,\
  COUNT(*) AS num_patients\
FROM patients\
GROUP BY city\
ORDER BY num_patients DESC, city asc;

#### 13. Show all allergies ordered by popularity. Remove NULL values from query.

**Solution**

SELECT\
  allergies,\
  count(allergies) AS total_diagnosis\
FROM patients\
GROUP BY allergies\
HAVING\
  allergies IS NOT NULL\
ORDER BY total_diagnosis DESC


SELECT\
  allergies,\
  count(allergies) AS total_diagnosis\
FROM patients\
GROUP BY allergies\
HAVING\
  allergies IS NOT NULL\
ORDER BY total_diagnosis DESC

SELECT\
  allergies,\
  count(*)\
FROM patients\
WHERE allergies NOT NULL\
GROUP BY allergies\
ORDER BY count(*) DESC

#### 14. Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.

**Solution**

select first_name, last_name,birth_date \
from patients \
where birth_date between '1970-01-01' and '1980-01-01'\
order by birth_date asc

SELECT\
  first_name,\
  last_name,\
  birth_date\
FROM patients\
WHERE\
  YEAR(birth_date) BETWEEN 1970 AND 1979
ORDER BY birth_date ASC;\

SELECT\
  first_name,\
  last_name,\
  birth_date\
FROM patients\
WHERE year(birth_date) LIKE '197%'\
ORDER BY birth_date ASC

#### 15. We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order EX: SMITH,jane

SELECT\
  CONCAT(UPPER(last_name), ',', LOWER(first_name)) AS new_name_format\
FROM patients\
ORDER BY first_name DESC;\

SELECT\
  UPPER(last_name) || ',' || LOWER(first_name) AS new_name_format\
FROM patients\
ORDER BY first_name DESC;

#### 16. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.

**Solution**

select province_id , sum(height) as sum_height\
from patients\
group by province_id\
having sum_height >= 7000;

#### 17. Show the difference between the largest weight and smallest weight for patients with the last name 'Maron

**Solution**

SELECT\
  (MAX(weight) - MIN(weight)) AS weight_delta\
FROM patients\
WHERE last_name = 'Maroni';