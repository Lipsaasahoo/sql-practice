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
