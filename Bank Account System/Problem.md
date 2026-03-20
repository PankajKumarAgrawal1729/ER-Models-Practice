## Bank Account System

A bank manages customers, accounts, and transactions. A customer can have multiple accounts. Accounts can be of different types. Transactions occur between accounts. This exercise focuses on IS-A hierarchies and ternary relationships.


### Requirements

- Each customer has a Customer ID, name, NIC number, address, and date of birth.
- Accounts can be Savings or Current (Checking). Both share Account Number and balance.
- Savings accounts have a minimum balance and interest rate.
- Current accounts have an overdraft limit.
- A customer can own multiple accounts. An account is owned by one or more customers (joint accounts).
- Each transaction has a Transaction ID, amount, timestamp, and type (Credit/Debit/Transfer).
- A transfer transaction involves a source account AND a destination account.


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 ACCOUNT should have two subtypes: SAVINGS_ACCOUNT and CURRENT_ACCOUNT (IS-A hierarchy)
- 💡 OWNS between CUSTOMER and ACCOUNT is M:N (joint accounts!)
- 💡 TRANSFER is a ternary relationship: TRANSACTION + SOURCE_ACCOUNT + DEST_ACCOUNT
- 💡 Or model TRANSFER as a binary relationship between two ACCOUNTs with TRANSACTION as a linking entity
- 💡 Customer address can be a composite attribute (street, city, postal code)
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>

<details>
<summary>ER Diagram</summary>
           
- [ER diagram]()
    </details>
 <details>
        <summary>Entities & Rels</summary>

- Entities
    - CUSTOMER
    - ACCOUNT
    - SAVINGS_ACCOUNT (subtype)
    - CURRENT_ACCOUNT (subtype)
    - TRANSACTION
- Relationships
    - OWNS CUSTOMER ↔ ACCOUNT (M:N)
        - Attributes: OpenedDate
    - IS-A / GENERALISATION ACCOUNT ↔ SAVINGS/CURRENT (Specialisation)
    - PERFORMS ACCOUNT ↔ TRANSACTION (1:N)
    - TRANSFER_TO (ternary) TRANSACTION ↔ SOURCE_ACCT ↔ DEST_ACCT (Ternary)
    </details>

    <details>
        <summary>Analysis</summary>

#### ✦ Key Concepts in This Exercise

##### IS-A (Specialisation) Hierarchy
- SAVINGS_ACCOUNT and CURRENT_ACCOUNT are both specialisations of ACCOUNT. They inherit all attributes of ACCOUNT and add their own. In ER diagrams, use a triangle labelled 'IS-A' connecting ACCOUNT to its subtypes. This is 'specialisation' (top-down) or 'generalisation' (bottom-up).

##### Composite Attribute — Address
- Address is a composite attribute: it has components (Street, City, PostalCode, Country). In ER notation, the composite attribute is an oval with sub-ovals connected to it. In SQL, this becomes multiple columns.

##### Ternary Relationship — Transfer
- A bank transfer involves three entities: the transaction, the source account, and the destination account. This is a ternary relationship (three-way). It's harder to model but more accurate than two separate binary relationships.

- ⚠️ Don't forget joint accounts — OWNS is M:N, not 1:N
- ⚠️ Don't put interest rate on the generic ACCOUNT — it belongs only on SAVINGS_ACCOUNT
- ⚠️ Overdraft limit only goes on CURRENT_ACCOUNT, not ACCOUNT
- ⚠️ A ternary relationship diamond connects to THREE entities — don't split it into two binary relationships unless you need to
    </details>
</details>

#### Self Assessment — How did your diagram compare?

- [x] I drew an IS-A hierarchy with ACCOUNT as supertype
- [x] I correctly placed specialised attributes on the subtype entities
- [x] I drew OWNS as M:N (to handle joint accounts)
- [x] I modelled TRANSFER as a ternary or correctly as two binary relationships
- [x] I drew Address as a composite attribute with sub-components