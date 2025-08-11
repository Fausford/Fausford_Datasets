# Fausford_Datasets
Locate all the datasets used in FAUSFORD_AI trainings in this repository

# Medical Dataset Overview


## Description 
 
Synthetic medical dataset simulating patient demographics, comorbidities, vitals, labs, and mortality.

Rows: 5,000 patients (randomly generated but following clinically plausible relationships).

Outcome: mortality (binary: 1 = patient died, 0 = survived).

Extra column: mortality_prob (continuous probability from the internal logistic risk model).

## Variable Dictionary

### 1. Demographics

age	Integer	Age in years (18–99). Older age increases risk for comorbidities and mortality.

sex	Categorical	"Male" or "Female". Males have slightly higher modeled mortality.

race	Categorical	"White", "Black", "Asian", "Other". Used only descriptively (no strong mortality coefficient).

### 2. Lifestyle / Social Factors

bmi	Float	Body mass index (15–60). Higher BMI raises hypertension & diabetes risk.

smoker	Binary (0/1)	Current or past smoker. Smoking increases COPD and mortality risk.

### 3. Comorbidities (Binary: 0 = absent, 1 = present)

hypertension	More likely with older age and higher BMI.

diabetes	More likely with higher BMI, older age, smoking.

copd	Strongly linked to smoking and older age.

ckd	Chronic kidney disease; linked to diabetes, hypertension, and older age.

cad	Coronary artery disease; linked to hypertension, diabetes, and older age.

cancer	Risk rises with age.

### 4. Vitals

systolic_bp	mmHg	Systolic blood pressure. Hypertension pushes it higher. Very low SBP increases mortality risk in model.

diastolic_bp	mmHg	Diastolic blood pressure.

heart_rate	bpm	Higher with CKD and age.

resp_rate	breaths/min	Higher with COPD and older age.

temperature_C	°C	Slightly higher in cancer.

spo2	%	Oxygen saturation. Lower with COPD and older age.

### 5. Laboratory Results

wbc	×10⁹/L	White blood cell count.

hemoglobin	g/dL	Lower in older patients and with chronic disease.

creatinine	mg/dL	Higher in CKD and older age.

glucose	mg/dL	Elevated in diabetes.

### 6. Outcomes

mortality	Binary	1 = death, 0 = survival.

mortality_prob	Continuous	Probability from internal logistic risk model. Not a “prediction” from ML training—this is the ground truth risk used to generate mortality.


Missingness: ~6% of selected non-outcome columns randomly missing, slightly more in survivors (mimicking missing-at-random patterns in real hospital data).

## File Details

File name: [medical_data](https://github.com/Fausford/Fausford_Datasets/blob/main/medical_synthetic.csv)

Format: CSV, UTF-8 encoded, comma-delimited.

Rows: 5,000

Columns: 24



# Dialysis Dataset Overview

## Description 

Synthetic patient dataset with emphasis on dialysis as a major outcome, **modeled** to be strongly tied to CKD (chronic kidney disease).

Rows: 5,000 patients.

Primary outcomes:

dialysis — binary: whether the patient received dialysis.

mortality — binary: whether the patient died.

Extra columns: dialysis_prob and mortality_prob — the “true” model probabilities used to generate outcomes.

##  Variable Dictionary

### 1. Demographics

age	Integer	Age in years (18–99). Older age increases CKD, dialysis, and mortality risk.

sex	Categorical	"Male" or "Female". Slightly higher mortality risk in males.

race	Categorical	"White", "Black", "Asian", "Other". Used descriptively.

bmi	Float	Body mass index (15–60). Higher BMI raises hypertension & diabetes risk.

smoker	Binary (0/1)	Smoking status. Higher COPD risk.

### 2. Comorbidities (Binary: 0 = absent, 1 = present)

hypertension	Higher in older and heavier patients. Risk factor for CKD and dialysis.

diabetes	Higher with higher BMI and age. Risk factor for CKD and dialysis.

copd	Linked to smoking and older age.

ckd	Chronic kidney disease; primary driver of dialysis probability.

cad	Coronary artery disease; linked to hypertension and diabetes.

cancer	More common in older patients.

### 3. Kidney Function Labs

creatinine	mg/dL	Higher in CKD patients. Strongly influences dialysis probability.

gfr	mL/min/1.73m²	Estimated glomerular filtration rate. Lower in CKD. Strong inverse effect on dialysis probability.

### 4. Outcomes

dialysis	Binary	1 = received dialysis, 0 = did not. Strongly related to CKD, high creatinine, low GFR, and comorbidities.

dialysis_prob	Continuous	Probability from the internal logistic model used to generate dialysis.

mortality	Binary	1 = death, 0 = survival. Increased by dialysis status, CKD, and other comorbidities.

mortality_prob	Continuous	Probability from the internal logistic model used to generate mortality.


Missingness
creatinine and gfr have ~5–10% missing values.

Missingness slightly more common among survivors, mimicking real-world patterns.

## File Details

File name: [dialysis_data](https://github.com/Fausford/Fausford_Datasets/blob/main/dialysis_synthetic.csv)

Format: CSV, UTF-8 encoded, comma-delimited.

Rows: 5,000

Columns: 17
