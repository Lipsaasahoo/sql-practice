# SQL Practice !

#### 1. Show first name and last name concatinated into one column to show their full name.

**Solution**

SELECT \
  CONCAT(first_name, '  ', last_name) AS full_name\
FROM patients;

SELECT first_name || ' ' || last_name\
FROM patients;