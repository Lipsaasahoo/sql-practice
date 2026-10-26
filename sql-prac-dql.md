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