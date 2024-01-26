# Education For All Fundraising Analysis

### Easily Access

[Project Overview](project-overview)

[Tools](tools)

[Exploratory Data Analysis](exploratory-data-analysis)

[Data Analysis](data-analysis)

[Results/Findings](results/findings)

[Recommendations](recommendations)

[View Analysis Report](view-analysis-report)


### Project Overview

Education For All is a charity organization whose mission is to ensure every student is able to access quality education irrespective of their economic background. This report focuses on analyzing the donation data from the previous year and gain insights to help the organization strategize and increase donations in future fundraising events.

### Tools

- PostgreSQL
 - Data Analysis

### Exploratory Data Analysis

The analysis answered some questions including but not limited to:

1. What is the total donation by gender?

2. What is the total donation made by donors in different job fields?

3. What is the total donation made by donors in different states?

4. Which states made the highest and least donations?

### Data Analysis

```SQL

SELECT * FROM donation_data;

SELECT * FROM donor_data;


-- a) How much is the total donation?

SELECT  SUM(donation) AS total_amount_donated,
		COUNT(donation)AS number_of_donations
FROM donation_data;

-- b) What is the total donation by gender?

SELECT
		SUM(CASE WHEN gender = 'Male' THEN donation ELSE 0 END) AS male_total_donation,
		SUM(CASE WHEN gender = 'Female' THEN donation ELSE 0 END) AS Female_total_donation
FROM donation_data;

-- c) Show the total donation and number of donations by gender.

SELECT 	dona.gender,
	COUNT(dona.donation) AS number_of_donations,
	SUM(CASE WHEN gender = 'Male' THEN donation ELSE 0 END) AS male_total_donations,
	SUM(CASE WHEN gender = 'Female' THEN donation ELSE 0 END) AS female_total_donations
FROM donation_data dona
GROUP BY dona.gender;

### Data Analysis

SQL

SELECT * FROM donation_data;

SELECT * FROM donor_data;


-- a) How much is the total donation?

SELECT  SUM(donation) AS total_amount_donated,
		COUNT(donation)AS number_of_donations
FROM donation_data;



-- b) What is the total donation by gender?

SELECT
		SUM(CASE WHEN gender = 'Male' THEN donation ELSE 0 END) AS male_total_donation,
		SUM(CASE WHEN gender = 'Female' THEN donation ELSE 0 END) AS Female_total_donation
FROM donation_data;



-- c) Show the total donation and number of donations by gender.

SELECT 	dona.gender,
	COUNT(dona.donation) AS number_of_donations,
	SUM(CASE WHEN gender = 'Male' THEN donation ELSE 0 END) AS male_total_donations,
	SUM(CASE WHEN gender = 'Female' THEN donation ELSE 0 END) AS female_total_donations
FROM donation_data dona
GROUP BY dona.gender;



-- d) Total donation made by frequency of donation.

SELECT

dono.donation_frequency,
		SUM(dona.donation) AS total_amount_donated
FROM donation_data dona
JOIN donor_data dono
ON dona.id = dono.id
GROUP BY dono.donation_frequency;


-- e) Total donation and number of donation by Job field.

SELECT
		job_field,
		SUM(donation) AS total_amount_donated,
		COUNT(donation) AS number_of_donations
FROM donation_data
GROUP BY job_field
ORDER BY total_amount_donated DESC;


-- f) Total donation and number of donations above $200.

SELECT
		SUM(donation) AS total_amount_donated,
		COUNT(donation) AS number_of_donations
FROM donation_data
WHERE donation > 200;


-- g) Total donation and number of donations below $200.

SELECT
		SUM(donation) AS total_amount_donated,
		COUNT(donation) AS number_of_donations
FROM donation_data
WHERE donation < 200;


-- h) Which top 10 states contributes the highest donations?


SELECT  state,
		SUM(donation) AS total_amount_donated
FROM donation_data
GROUP BY state
ORDER BY total_amount_donated DESC
LIMIT 10;


-- i) Which top 10 states contributes the least donations?

SELECT  state,
		SUM(donation) AS total_amount_donated
FROM donation_data
GROUP BY state
ORDER BY total_amount_donated ASC
LIMIT 10;


### Data Analysis

SQL

SELECT * FROM donation_data;

SELECT * FROM donor_data;


-- a) How much is the total donation?

SELECT  SUM(donation) AS total_amount_donated,
		COUNT(donation)AS number_of_donations
FROM donation_data;



-- b) What is the total donation by gender?

SELECT
		SUM(CASE WHEN gender = 'Male' THEN donation ELSE 0 END) AS male_total_donation,
		SUM(CASE WHEN gender = 'Female' THEN donation ELSE 0 END) AS Female_total_donation
FROM donation_data;



-- c) Show the total donation and number of donations by gender.

SELECT 	dona.gender,
	COUNT(dona.donation) AS number_of_donations,
	SUM(CASE WHEN gender = 'Male' THEN donation ELSE 0 END) AS male_total_donations,
	SUM(CASE WHEN gender = 'Female' THEN donation ELSE 0 END) AS female_total_donations
FROM donation_data dona
GROUP BY dona.gender;



-- d) Total donation made by frequency of donation.

SELECT

dono.donation_frequency,
		SUM(dona.donation) AS total_amount_donated
FROM donation_data dona
JOIN donor_data dono
ON dona.id = dono.id
GROUP BY dono.donation_frequency;


-- e) Total donation and number of donation by Job field.

SELECT
		job_field,
		SUM(donation) AS total_amount_donated,
		COUNT(donation) AS number_of_donations
FROM donation_data
GROUP BY job_field
ORDER BY total_amount_donated DESC;


-- f) Total donation and number of donations above $200.

SELECT
		SUM(donation) AS total_amount_donated,
		COUNT(donation) AS number_of_donations
FROM donation_data
WHERE donation > 200;



-- g) Total donation and number of donations below $200.

SELECT
		SUM(donation) AS total_amount_donated,
		COUNT(donation) AS number_of_donations
FROM donation_data
WHERE donation < 200;



-- h) Which top 10 states contributes the highest donations?


SELECT  state,
		SUM(donation) AS total_amount_donated
FROM donation_data
GROUP BY state
ORDER BY total_amount_donated DESC
LIMIT 10;



-- i) Which top 10 states contributes the least donations?

SELECT  state,
		SUM(donation) AS total_amount_donated
FROM donation_data
GROUP BY state
ORDER BY total_amount_donated ASC
LIMIT 10;



-- j) What are the top 10 cars driven by the highest donors?

SELECT  dona.id,
		dona.first_name,
		dona.last_name,
		dona.donation AS total_amount_donated,
		dono.car
FROM donation_data dona
JOIN donor_data dono
ON dona.id = dono.id
ORDER BY total_amount_donated DESC
LIMIT 10;
```


### Results/Findings

1. Total amount donated is $249,085 and a total of 1000 donations were made.

2. Male donors donated $127,628 in 492 donations.

3. Female donors donated $121,457 in 508 donations.

4. More donations were made Yearly, amounting to $35,266 while the least donations were made monthly, amounting to $26,870

5. The highest donations were made by donors in Human Resources job field at $23,060 followed by Research and Development job field at $22,862, and Product Management job field at $22,798.

6. Total donations above $200 is $205,892 

7. Total donations below  $200 is $42,593

8. States with the highest donations are California, Texas and Florida at $30,264, $24,097 and $20,562 respectively.

9. States with the least donations are Wyoming, Maine and South Dakota with a total of $232, $258 and $401 donations respectively.

10. Cars driven by the highest donors are Ford by Beverlie Andriess ($500), Lexus by Wallie Leather ($500) and Mazda by Peder Rilton ($499).


### Recommendations

1. Fundraising campaigns should be organized to appeal a broader audience. The positive impact of donations and how they contribute to the success of  Education For All should be greatly highlighted.

2. Consistent monthly donations should be encouraged through a structured program and monthly educational events. The program should highlight the impact of continuous support on advancing education accessibility while showcasing the urgency of support.

3. Donors who contributed above $200 should be acknowledged and appreciated. An award event could be held annually to acknowledge donors and   show them a few outstanding beneficiaries of the Education For All Charity. This would spur donors to do more seeing that their contributions are put into good use.

Summarily, donors should be educated on the significance of their contributions by sharing success stories and showing how their donations have impacted or will impact the mission of Education For All Charity.

### View Analysis Report

To view screenshots of analysis on a pdf file, [Click here.]()
