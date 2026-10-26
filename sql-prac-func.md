#### 1.Show how many patients have a birth_date with 2010 as the birth year.

**Solution**

SELECT count(patient_id) as total_patients  FROM patients where birth_date like "2010-%" 

SELECT COUNT(*) AS total_patients \ 
FROM patients \
WHERE YEAR(birth_date) = 2010;

SELECT count(first_name) AS total_patients \
FROM patients \
WHERE \
  birth_date >= '2010-01-01' \
  AND birth_date <= '2010-12-31'

SELECT count(first_name) AS total_patients \
FROM patients \
WHERE \
  birth_date between '2010-01-01' AND '2010-12-31'



#### 2. Show the first_name, last_name, and height of the patient with the greatest height.

**Solution**

select \
	first_name, \
    last_name, \
    max(height) as height \
from patients

SELECT \
  first_name, \
  last_name, \
  height \
FROM patients \
WHERE height = ( \
    SELECT max(height) \
    FROM patients\
  )


#### 3. Show the total number of admissions

**Solution**

SELECT count(*) as total FROM admissions


#### 4. Show the patient id and the total number of admissions for patient_id 579.


**Solution**

SELECT \
  patient_id, \
  COUNT(*) AS total_admissions \
FROM admissions \
WHERE patient_id = 579;