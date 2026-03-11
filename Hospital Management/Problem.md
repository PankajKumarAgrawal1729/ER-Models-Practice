## Hospital Management

A hospital tracks patients, doctors, and wards. Patients are admitted to wards and treated by doctors. Each ward has a nurse in charge. This is a classic ER exercise used in database courses worldwide.


### Requirements

- Each patient has a Patient ID, name, date of birth, and blood type.
- Each doctor has an Employee ID, name, specialisation, and contact number.
- Each ward has a Ward Number, ward name, and capacity.
- A patient is admitted to one ward at a time. A ward can hold many patients.
- A patient can be treated by multiple doctors. A doctor can treat multiple patients
- Each treatment has a diagnosis, start date, and end date.
- Each ward has exactly one nurse-in-charge (also an employee with ID, name).


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 PATIENT–WARD is 1:N (one ward, many patients — but one patient in one ward at a time)
- 💡 PATIENT–DOCTOR is M:N with attributes (diagnosis, dates) on the TREATS relationship
- 💡 NURSE is a separate entity (or can be a specialised entity under EMPLOYEE)
- 💡 Ward has a 1:1 relationship with the Nurse-in-Charge
- 💡 BloodType on PATIENT is a good single-valued attribute example
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>

<details>
<summary>ER Diagram</summary>
           
- [ER diagram](https://github.com/PankajKumarAgrawal1729/ER-Models-Practice/blob/main/Hospital%20Management/ERDiagram.png)
    </details>
 <details>
        <summary>Entities & Rels</summary>

- Entities
    - PATIENT
    - DOCTOR
    - WARD
    - NURSE
- Relationships
    - ADMITTED_TO PATIENT ↔ WARD (N:1)
    - ATREATS DOCTOR ↔ PATIENT (M:N)
        - Attributes: Diagnosis, StartDate, EndDate
    - MANAGED_BY WARD ↔ NURSE (1:1)
    </details>

    <details>
        <summary>Analysis</summary>

#### ✦ Key Concepts in This Exercise

##### ISA / Generalisation (Optional Extension)
- DOCTOR and NURSE could both be specialisations of EMPLOYEE entity using an IS-A hierarchy. This is called generalisation — you'd have EMPLOYEE as the supertype with shared attributes (EmployeeID, Name), and DOCTOR/NURSE as subtypes with specialised attributes.

##### Treatment Attributes on Relationship
- Diagnosis and dates belong to TREATS, not to PATIENT or DOCTOR alone. A diagnosis is specific to a particular doctor treating a particular patient at a particular time.

##### 1:1 Relationship
- WARD to NURSE-IN-CHARGE is 1:1 — this is rarer than 1:N or M:N but important to recognise. Show total participation on both sides since every ward must have a nurse-in-charge.

- ⚠️ Don't confuse DOCTOR–PATIENT cardinality: it's M:N, not 1:N
- ⚠️ PATIENT being in ONE ward at a time makes ADMITTED_TO N:1, not M:N
- ⚠️ If you merge DOCTOR and NURSE into EMPLOYEE, still model the different relationships separately
    </details>
</details>
