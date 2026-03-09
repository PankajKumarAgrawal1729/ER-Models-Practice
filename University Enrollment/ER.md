## University Enrollment

A university needs to track students, courses, and instructors. Students enroll in courses, and each course is taught by one instructor. A student can enroll in multiple courses, and a course can have many students.


### Requirements

- Each student has a Student ID, name, email, and date of birth.
- Each course has a Course Code, title, credits, and department.
- Each instructor has an Employee ID, name, office number, and phone number.
- A student can enroll in many courses; a course can have many students enrolled.
- Each course is taught by exactly one instructor.
- An instructor may teach zero or more courses.
- The enrollment has an attribute: enrollment date and grade.


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 STUDENT and COURSE have a M:N relationship — needs an associative entity or relationship with attributes
- 💡 INSTRUCTOR to COURSE is 1:N (one instructor teaches many courses)
- 💡 StudentID, CourseCode, and EmployeeID are your primary keys
- 💡 Enrollment date and grade are attributes OF the Enrolls relationship
- 💡 Age can be a derived attribute computed from date of birth
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>
    <details>
        <summary>ER Diagram</summary>

        - [ER diagram](University%20Enrollment/.excalidraw)
    </details>
    <details>
        <summary>Entities & Rels</summary>
        
        - Entities
            - Student
            - Course
            - Instructor
        - Relationships
            - ENROLLS: STUDENT ↔ COURSE (M:N)
                - Attributes: EnrollDate, Grade
            - TEACHES: INSTRUCTOR ↔ COURSE (1:N)
    </details>
    <details>
        <summary>Analysis</summary>

        #### ✦ Key Concepts in This Exercise

        ##### M:N Relationship with Attributes
        - The ENROLLS relationship has its own attributes (grade, enrollment date). This is important: you CANNOT just put these on the entities — they belong to the relationship itself.

        ##### 1:N vs M:N
        - TEACHES is 1:N because a course has exactly one instructor. ENROLLS is M:N because many students can be in one course and one student can be in many courses.

        ##### Derived Attribute
        - Age is a derived attribute (dashed oval) because it can be calculated from DateOfBirth. Never store both — store the source and derive the result.

        - ⚠️ Don't put grade/enrollment date on STUDENT or COURSE — they belong to the ENROLLS relationship
        - ⚠️ Course is NOT a weak entity even though it needs an instructor — it has its own primary key (CourseCode)
        - ⚠️ Don't forget total participation: every COURSE must have an instructor (double line on COURSE side of TEACHES)
    </details>
</details>
