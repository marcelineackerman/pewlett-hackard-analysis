# Pewlett-Hackard Analysis

## Overview of Project

An analysis of employee data for the company Pewlett-Hackard in order to predict and prepare for the upcoming wave of retirees, using PostgreSQL.

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
