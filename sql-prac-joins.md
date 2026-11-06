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


#### 3. Show first name, last name and role of every person that is either patient or doctor.The roles are either "Patient" or "Doctor"

**Solution**

SELECT first_name, last_name, "Patient" as role \
FROM patients\
union all \
SELECT first_name, last_name, "Doctor" as role\
FROM doctors

#### 4. Show first_name, last_name, and the total number of admissions attended for each doctor.Every admission has been attended by a doctor.

**Solution**

select first_name, last_name, count(*) as admissions_total\
from doctors \
join admissions \
on doctors.doctor_id = admissions.attending_doctor_id \
group by attending_doctor_id

#### 5. For each doctor, display their id, full name, and the first and last admission date they attended.

**Solution**

select doctor_id, concat(first_name, ' ', last_name) as full_name, \
min(admission_date) as first_admission_date, max(admission_date) as last_admission_date \
from doctors \
join admissions \
on doctors.doctor_id = admissions.attending_doctor_id \
group by attending_doctor_id

#### 6. Display the total amount of patients for each province. Order by descending.

**Solution**

select province_name, count(*) as patient_count \
from province_names \
join patients \
on province_names.province_id = patients.province_id \
group by province_name \
order by patient_count desc