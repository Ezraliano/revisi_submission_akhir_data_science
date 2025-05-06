SELECT
    "index" AS id,
    
    -- Marital status mapping
    CASE "Marital_status"
        WHEN '1' THEN 'Single'
        WHEN '2' THEN 'Married'
        WHEN '3' THEN 'Widowed'
        WHEN '4' THEN 'Divorced'
        ELSE 'Other'
    END AS marital_status,

    "Gender",
    "Age_at_enrollment",
    "Nacionality",
    "Mothers_qualification",
    "Fathers_qualification",
    "Mothers_occupation",
    "Fathers_occupation",
    "Scholarship_holder",
    "Educational_special_needs",
    "Displaced",
    "Application_mode",
    "Application_order",
    "Course",
    "Daytime_evening_attendance",
    "Previous_qualification",
    "Previous_qualification_grade",
    "Admission_grade",
    "Debtor",
    "Tuition_fees_up_to_date",
    "GDP",
    "Unemployment_rate",
    "Inflation_rate",
    
    "Curricular_units_1st_sem_approved",
    "Curricular_units_1st_sem_grade",
    "Curricular_units_2nd_sem_approved",
    "Curricular_units_2nd_sem_grade",

    -- Kolom turunan: nilai rata-rata akademik
ROUND((
    COALESCE("Curricular_units_1st_sem_grade", 0)::numeric +
    COALESCE("Curricular_units_2nd_sem_grade", 0)::numeric
) / 2, 2) AS avg_academic_score,

    -- Kolom turunan: status keberhasilan
    CASE "Status"
        WHEN 'Enrolled' THEN 'Active'
        WHEN 'Graduate' THEN 'Completed'
        WHEN 'Dropout' THEN 'Left'
        ELSE 'Unknown'
    END AS student_status

FROM "orders";
