# Pewlett-Hackard-Analysis

Overview

This analysis uses SQL to determine the number of employees that are slated to retire from Pewlett-Hackard and also identifies individuals who are eligible for the mentorship program. 

The first part of the analysis pulled the number of retiring employees by job title, unique employee ID number, and start and end dates for employment. Finally a filter was applied to identify employees born between 1952 and 1955 to better identify those eligible for retirement.

The second part of the analysis focuses on employees born in 1965 who are eligible to serve as mentors in the mentorship program.




Results

- The data shows that 90,398 employees are currently eligible for retirement

- 50% of the workforce eligible for retirement are Engineers

- Of the 90,398 employees eligible for retirement, over 60% are of Senior Staff as seen in the summary table below

![image](https://user-images.githubusercontent.com/112994018/198164433-2f78c76f-7b1a-45da-afb6-9f33e887e7d1.png)


- There are also currently 1,549 employees that are eligible to serve as Mentors



![image](https://user-images.githubusercontent.com/112994018/198164471-3800f918-1afe-48e7-8f45-ec0c6eb891df.png)


Summary

Findings reveal that there will be 90,398 open positions in the near future due to expected retirements. This could indicate a gap in the near future meaning more workforce training programs to promote Junior staff may be needed. 

There are currently 1,549 employees eligible for the Mentorship program. While this number is good, there may still be a gap to cover the over 300,000 employees within the company. 

Additional queries that may be helpful to build upon the analysis includes the following:

- Since Senior Engineers represent the largest group where retirements will occur, the following query would be useful to help determine the number of Senior Engineers eligible for the Mentorship Program in an effort to match them with current Junior Engineers who can fulfill the future roles:

SELECT DISTINCT ON (e.emp_no) e.emp_no,
    e.first_name,
	e.last_name,
	e.birth_date,
	de.from_date,
	de.to_date,
	ti.title
--INTO mentorship_eligibility
FROM employees as e
INNER JOIN dept_emp as de
ON (e.emp_no = de.emp_no)
INNER JOIN titles as ti
ON (e.emp_no = ti.emp_no)
WHERE (de.to_date = '9999-01-01')
AND (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
AND ti.title = ('Senior Engineer')

--Also to proactively plan, it may be helpful to identify the next batch of employees eligible for retirement by running a query employees born between 1956 and 1959. The could help the company proactively plan to train and fill positions moving forward:

Select e.emp_no,
    e.first_name,
	e.last_name,
	ti.title,
	ti.from_date,
	ti.to_date
--Into retirement_titles
FROM employees as e
INNER JOIN titles as ti
ON (e.emp_no = ti.emp_no)
WHERE (e.birth_date BETWEEN '1956-01-01' AND '1959-12-31')
ORDER by emp_no;

