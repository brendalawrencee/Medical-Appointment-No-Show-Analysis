# <p align="center">Medical Appointment No-Show Analysis</p>
# <p align="center">![Pic](https://face2facehr.com/wp-content/uploads/2016/11/Medical-appointments-web.jpg)</p>

<img width="2798" height="1598" alt="Appointment No-Show Dashboard" src="https://github.com/user-attachments/assets/cf01bb3d-2f91-49de-b3ab-65b8698ee631" />

[View this Dashboard on Tableau!](https://public.tableau.com/views/MedicalAppointmentNo-ShowDashboard/AppointmentNo-ShowDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)



## Business Problem: 
Medical appointment no-shows cause major problems for both patient health and clinic operations. This project looks at data from 110,527 medical appointments in Brazil to find which appointment characteristics are linked to higher no-show rates. The goal is to help clinics and hospitals identify ways to reduce appointment no-show rates, helping both patient and clinic outcomes.


## Data & Tools:
- **Dataset**: https://www.kaggle.com/datasets/joniarroba/noshowappointments/data 
- **Database**: MySQL Workbench
- **Techniques Used**: Aggregation, Conditional logic, Window Functions, CTEs and views. 

## Approach/Methodology:
**Cleaning**: Started by reviewing the dataset structure and sample records, renamed unclear or misspelled columns to make the data easier to work with, converted dates into appropriate formats, created a lead time variable showing the number of days between scheduling and the appointment, checked for invalid values including negative lead times and an age value of -1 and removed invalid records.

**Exploratory Analysis**: Calculated the overall no-show rate and compared it across different factors including: Day of the week, Appointment lead time, Age groups, SMS reminder status, Neighbourhoods. 

**Advanced Analysis**: Used window functions to track each patient's previous appointments and no-shows, then used a CTE to calculate prior no-show rates. Built a reusable SQL view that combined prior no-show rate and appointment lead time to assign appointments to different risk tiers.

**Findings**: Summarized the results into three key findings that connect back to the main business problem.

## Key SQL Techniques Used:
- Data cleaning and transformation: ALTER TABLE, UPDATE, STR_TO_DATE(), REPLACE(), DATEDIFF() and DELETE
- Data validation: MIN(), MAX(), COUNT(), filtering for invalid/negative values
- Aggregation: COUNT(), SUM(), ROUND(), GROUP BY, HAVING
- Conditional logic: CASE WHEN to create age groups, lead-time categories and risk tiers
- Subqueries: Calculating percentages against the total number of appointments
- Window functions: COUNT() OVER(), SUM() OVER(), and RANK() OVER() to analyze patient history and rank neighbourhoods
- CTEs and views: Created a reusable v_appointment_risk view using a CTE to organize patient-level risk analysis


## Findings 
1. **Lead time matters significantly**. Appointments with higher lead times (time between when the appointment was scheduled to when the actual appointment was) had the highest no-show rates.
2. Saturday had the highest no-show rate however it had significantly less appointments. While Tuesday and Wednesday had the most number of appointments and lower no-show rates.
3. SMS notifications were interesting as patients that received SMS reminders had higher no-show rates. However, this is relation is not evident of causation when taking into account Lead Time of those appointments that received SMS reminders.
- When taking into consideration Lead Time, appointments that did not receive SMS reminders had higher no-show rates.


## Recommendations
- Suggest clinics **take longer lead times into consideration** when appointment scheduling and explore ways to reduce lead times from both the clinic and patient sides.
- Provide extra scheduling coordination and reminders to patients with higher no-show risk based on their prior no-shows and lead time.
- Review SMS notifications for longer lead times and explore multiple reminders to provide more consistent follow-up before appointments.


  
