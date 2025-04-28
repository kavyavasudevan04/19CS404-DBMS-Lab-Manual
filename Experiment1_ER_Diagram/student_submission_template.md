# ER Diagram Submission - Student Name Kavya.V

## Scenario Chosen:
Hospital

## ER Diagram:
![image](https://github.com/user-attachments/assets/f22216ec-5ee5-4b50-8411-917e44f5296d)


## Entities and Attributes:
#### DEPARTMENT
Attributes: dept_id (Primary Key), dept_head, dept_name

#### DOCTOR
Attributes: doctor_id (Primary Key), name, specialization, phone_no, email_id, work_schedule

#### PATIENT
Attributes: patient_id (Primary Key), name, dob, gender, phone_no, email, insurance_details, address (door_no, street, district)

#### APPOINTMENT
Attributes: appointment_id (Primary Key), appointment_time&date, reason_for_visit

#### MEDICAL_RECORDS
Attributes: record_id (Primary Key), diagnosis, treatment, medication, result

#### BILLING
Attributes: billing_id (Primary Key), amount, date

#### PAYMENT
Attributes: payment_id (Primary Key), payment_method, payment_mode, payment_status, amount_paid

## Relationships and Constraints:
#### Relationship1: DEPARTMENT — has — DOCTOR
```
Cardinality: 1:N (One department can have many doctors)
Participation: Total on DOCTOR side (Every doctor belongs to a department)
```

#### Relationship2: DOCTOR — have — APPOINTMENT
```
Cardinality: 1:N (One doctor can have many appointments)
Participation: Partial (Not all doctors may have appointments at a time)
```

#### Relationship3: PATIENT — have — APPOINTMENT
```
Cardinality: 1:N (One patient can have multiple appointments)
Participation: Total on PATIENT side (Appointments require patients)
```

#### Relationship4: APPOINTMENT — have — MEDICAL_RECORDS
```
Cardinality: 1:1 or 1:N (One appointment leads to one or more medical records)
Participation: Total on both sides
```

#### Relationship5: APPOINTMENT — have — BILLING
```
Cardinality: 1:1 (Each appointment generates one billing entry)
Participation: Total on both sides
```

#### Relationship6: BILLING — have — PAYMENT
```
Cardinality: 1:N (One billing can have multiple payments, for example, partial payments)
Participation: Partial on PAYMENT side (Not all bills may be fully paid immediately)
```
## Extension (Prerequisite / Billing):
#### Billing as Prerequisite Extension:
```
After an appointment, a billing must occur.
Billing contains the amount due based on the service/consultation.
A payment is mandatory after a billing (full or partial).
This ensures that the flow of data from appointment → billing → payment is continuous and mandatory for process completion.
```
## Design Choices:
#### Entities:
```
Entities like PATIENT, DOCTOR, and DEPARTMENT are natural choices in a hospital system.
BILLING and PAYMENT are modeled separately because payments can be made in parts (for instance, insurance covers part and patient pays the rest).
MEDICAL_RECORDS are linked to appointments to maintain the patient's diagnosis history systematically.
```

#### Relationships:
```
The cardinality and participation are designed considering real-world hospital scenarios.
Every appointment must have a patient and doctor involved.
Every billing must link to an appointment.
Every payment must reference billing but billing might initially be unpaid.
```

#### Assumptions:
```
A department must have at least one doctor.
A patient must exist before an appointment is made.
Payment may not happen immediately after billing.
Every appointment generates a medical record.
```






