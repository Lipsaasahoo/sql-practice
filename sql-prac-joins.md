# SQL Practice !

#### 1. Show first name, last name, and the full province name of each patient.Example: 'Ontario' instead of 'ON'

**Solution**

SELECT\
  first_name,\
  last_name,\
  province_name\
FROM patients\
  JOIN province_names ON province_names.province_id = patients.province_id;

#### 2. Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.Primary diagnosis is stored in the admissions table.

**Solution**

select p.patient_id, p.first_name, p.last_name \
from patients as p \
Inner join admissions as a \
on p.patient_id = a.patient_id \
where diagnosis = 'Dementia' \

SELECT \
  patient_id, \
  first_name, \
  last_name \
FROM patients \
WHERE patient_id IN ( \
    SELECT patient_id \
    FROM admissions \
    WHERE diagnosis = 'Dementia' \
  ); \

SELECT \
  patient_id, \
  first_name, \
  last_name \
FROM patients p \
WHERE 'Dementia' IN ( \
    SELECT diagnosis \
    FROM admissions \
    WHERE admissions.patient_id = p.patient_id \
  ); \