# Pewlett-Hackard Analysis

## Overview of Project

An analysis of employee data for the company Pewlett-Hackard in order to predict and prepare for the upcoming wave of retirees, using PostgreSQL.

## Resouces

 - PostgreSQL 11, pgAdmin 4

## Results and Findings

 - The most immediate and urgent finding is that a truly massive amount of employees are on the verge of retirement.

![image](https://user-images.githubusercontent.com/100869713/167918307-1fe13e0a-00f4-4e67-a6d4-b9deef85e12c.png)


 - A large majority of retirees will be coming from senior staff and engineers. This could mean a large loss of irreplacable institutional knowledge.

 - There are a number of younger staff eligible to be mentored by leaving staff, if the potential retirees agree to stay on as part-time mentors rather than completely retire.


- The last finding concerns the difference between mentorship-eligible employees and potential retirees. There are a number of employees eligible, and could have a head start in preserving the institutional knowledge of the staff leaving.
![image](https://user-images.githubusercontent.com/100869713/167923316-fc4de7f9-9b4c-4d48-a7ec-c737f1f1b6f5.png)


## Summary
Using the following query, we can see that there are 72,458 potential retirees in the upcoming "silver tsunami", in need of replacement if we keep the workforce even:
```
SELECT COUNT(emp_no) FROM unique_titles;
```
![image](https://user-images.githubusercontent.com/100869713/167918849-7a5efbfe-5967-44f8-9254-d0169a187ccc.png)

Utilizing the following query, we can see the total number of employees in the company is 300,024.

```
SELECT COUNT(DISTINCT emp_no) FROM employees;
```
![image](https://user-images.githubusercontent.com/100869713/167919532-f55c8040-2a82-45ed-a4f6-211ef6eac857.png)

This is a massive **24%** decrease in workforce over the next few years as these employees retire.

Utilizing another COUNT query, we can see that there are roughly **1,549** employees eligible for mentoring. With over 70,000 employees leaving, this means only **2%** of retirees would be able to stay on, if they agreed to become mentors. This means potential mentors must be chosen very carefully from senior staff.

```
SELECT COUNT(emp_no) FROM mentorship_eligibility;
```
![image](https://user-images.githubusercontent.com/100869713/167920798-22e789f9-fcca-490c-8238-7040c76ddadd.png)

This is obviously nowhere near enough to replace the upcoming loss of workforce. The original mentorship query was for employees born in the year 1965. If we increase that range, and make even younger employees eligible for mentorship, we may have more success in filling these senior leadership roles over time.

```
SELECT DISTINCT ON (e.emp_no) e.emp_no,
	e.first_name,
	e.last_name,
	e.birth_date,
	de.from_date,
	de.to_date,
	ti.title
INTO mentorship_eligibility_two
FROM employees as e
	INNER JOIN dept_emp as de
		ON (e.emp_no = de.emp_no)
	INNER JOIN titles as ti
		ON (e.emp_no = ti.emp_no)
	WHERE (de.to_date = '9999-01-01')
	AND (e.birth_date BETWEEN '1965-01-01' AND '1990-12-31')
ORDER BY e.emp_no ASC
```
![image](https://user-images.githubusercontent.com/100869713/167924457-ed2903e8-0be6-46e3-bf9b-7648aa0143fc.png)

```
SELECT COUNT(emp_no) FROM mentorship_eligibility_two;
```
![image](https://user-images.githubusercontent.com/100869713/167924480-e7d66791-c788-43dc-ad27-5311e822689c.png)

Unfortunately, there do not seem to be any employees born *after* 1965 within the company structure at all. This could spell disaster over the next few decades as more and more employees retire. Pewlett-Hackard must consider hiring a younger workforce, both to mitigate possible disaster and to keep up with the competitive job market.
