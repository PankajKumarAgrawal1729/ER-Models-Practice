## Library System

A public library manages books, members, and loans. Books can have multiple authors and multiple copies. Members can borrow copies and place holds on books. This exercise focuses on multi-valued attributes and distinguishing between a BOOK and a BOOK_COPY.


### Requirements

- Each book has an ISBN, title, genre, and publication year. A book can have multiple authors.
- Each physical copy has a Copy ID, condition (Good/Fair/Poor), and acquisition date.
- Each member has a Member ID, name, email, phone, and membership expiry date.
- A member borrows a copy (not a book). A copy can be borrowed by one member at a time.
- Each loan has a loan date, due date, and return date (null if not returned).
- Members can place holds/reservations on books (not specific copies).
- Each author has an Author ID and name. An author can write many books.


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 BOOK and BOOK_COPY are two separate entities — one is the conceptual work, the other a physical item
- 💡 WRITTEN_BY between BOOK and AUTHOR is M:N
- 💡 BORROWS is between MEMBER and BOOK_COPY (not BOOK), and it's M:N with loan attributes
- 💡 HOLDS/RESERVES is between MEMBER and BOOK (the concept, not a specific copy)
- 💡 Return date being nullable is a business rule, not an ER modelling concern
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>

<details>
<summary>ER Diagram</summary>
           
- [ER diagram](https://github.com/PankajKumarAgrawal1729/ER-Models-Practice/blob/main/Library%20System/ERDiagram.png)
    </details>
 <details>
        <summary>Entities & Rels</summary>

- Entities
    - BOOK
    - BOOK_COPY (weak)
    - AUTHOR
    - MEMBER
- Relationships
    - WRITTEN_BY BOOK ↔ AUTHOR (M:N)
    - HAS_COPY (identifying) BOOK ↔ BOOK_COPY (1:N)
    - BORROWS MEMBER ↔ BOOK_COPY (M:N)
        - Attributes: LoanDate, DueDate, ReturnDate
    - HOLDS MEMBER ↔ BOOK (M:N)
        - Attributes: HoldDate, Position
    </details>

    <details>
        <summary>Analysis</summary>

#### ✦ Key Concepts in This Exercise

##### BOOK vs BOOK_COPY Distinction
- This split is crucial in library systems. BOOK (ISBN, Title) is the intellectual work. BOOK_COPY (CopyID, Condition) is the physical object you actually loan. Members borrow COPIES, but place holds on BOOKS.

##### BORROWS as M:N with History
- BORROWS is M:N because over time, a member borrows many copies, and a copy is borrowed by many different members. Loan date, due date, and return date are attributes of BORROWS — they describe a specific lending event.

##### Author as Separate Entity
- Author should be a separate entity (not just an attribute) because authors have their own data (Author ID, name) and the WRITTEN_BY relationship is M:N. If it were stored as an attribute, you'd violate 1NF by having multiple author names in one field.

- ⚠️ Don't store Author as a multi-valued attribute — it should be a separate entity since authors have their own identity
- ⚠️ Don't make BORROWS between MEMBER and BOOK — you borrow physical copies, not the concept of a book
- ⚠️ BOOK_COPY is a weak entity because a copy has no meaning without its parent BOOK
- ⚠️ Don't forget MembershipExpiryDate is a derived-adjacent attribute — it changes over time but isn't truly derived
    </details>
</details>


#### Self Assessment — How did your diagram compare?

- [x] I separated BOOK and BOOK_COPY as distinct entities
- [x] I drew BOOK_COPY as a weak entity dependent on BOOK
- [x] I drew BORROWS between MEMBER and BOOK_COPY (not BOOK)
- [x] I drew HOLDS between MEMBER and BOOK
- [x] I placed loan attributes (LoanDate, DueDate, ReturnDate) on the BORROWS relationship