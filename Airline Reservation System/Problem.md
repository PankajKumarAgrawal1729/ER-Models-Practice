## Airline Reservation System

An airline manages flights, aircraft, passengers, and reservations. This is a complex real-world scenario that tests all ER concepts: weak entities, ISA hierarchies, composite keys, ternary relationships, and multi-valued attributes.


### Requirements

- Each flight has a Flight Number, departure airport, arrival airport, departure time, and arrival time.
- Each aircraft has a Registration Number, model, manufacturer, and seating capacity.
- Each flight is operated by one aircraft. An aircraft can operate many flights.
- Each passenger has a Passport Number, name, nationality, and date of birth.
- A passenger makes a reservation for a specific flight. A reservation has a Reservation ID, booking date, status, and seat number.
- Flights have Crew: pilots and cabin crew. Crew are employees with Employee ID, name, and role.
- Each flight has exactly one pilot-in-command (Captain). A flight can have multiple cabin crew.
- Airports have an IATA Code, name, city, and country.


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 RESERVATION could be a weak entity — it depends on both PASSENGER and FLIGHT
- 💡 AIRPORT appears twice (departure and arrival) — use role labels on the FLIGHT–AIRPORT relationship
- 💡 CREW has a IS-A: PILOT and CABIN_CREW are subtypes of CREW/EMPLOYEE
- 💡 The DEPARTS_FROM and ARRIVES_AT are two separate relationships from FLIGHT to AIRPORT (with role labels)
- 💡 Seat number belongs on RESERVATION (not FLIGHT or PASSENGER) — a seat is for a specific passenger on a specific flight
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>

<details>
<summary>ER Diagram</summary>
           
- [ER diagram](https://github.com/PankajKumarAgrawal1729/ER-Models-Practice/blob/main/Airline%20Reservation%20System/ERDiagram.png)
    </details>
 <details>
        <summary>Entities & Rels</summary>

- Entities
    - FLIGHT
    - AIRCRAFT
    - PASSENGER
    - RESERVATION (weak)
    - AIRPORT
    - EMPLOYEE/CREW
    - PILOT (subtype)
    - CABIN_CREW (subtype)
- Relationships
    - OPERATED_BY FLIGHT ↔ AIRCRAFT (N:1)
    - MAKES PASSENGER ↔ RESERVATION (1:N)
    - FOR_FLIGHT (identifying) RESERVATION ↔ FLIGHT (N:1)
    - DEPARTS_FROM FLIGHT ↔ AIRPORT (N:1)
    - ARRIVES_AT FLIGHT ↔ AIRPORT (N:1)
    - COMMANDS PILOT ↔ FLIGHT (1:N)
    - STAFFS CABIN_CREW ↔ FLIGHT (M:N)
    </details>

    <details>
        <summary>Analysis</summary>

#### ✦ Key Concepts in This Exercise

##### FLIGHT uses AIRPORT twice — Role Labels Required
- FLIGHT has a departure airport AND an arrival airport. This creates two separate relationships from FLIGHT to AIRPORT: DEPARTS_FROM and ARRIVES_AT. Both are N:1 (many flights depart from one airport). Role labels are mandatory here to distinguish the two participation roles of AIRPORT.

##### RESERVATION as Weak Entity
- RESERVATION can be modelled as a weak entity because its existence depends on both a PASSENGER and a FLIGHT. Its discriminator might be the booking sequence number. The identifying relationship connects it to FLIGHT (its owner).

##### Complex IS-A: PILOT and CABIN_CREW
- PILOT and CABIN_CREW are specialisations of EMPLOYEE. PILOT has one relationship (COMMANDS a FLIGHT — 1:N). CABIN_CREW has another (STAFFS a FLIGHT — M:N). These distinct cardinalities justify keeping them as separate subtypes.

- ⚠️ AIRPORT must appear ONCE as an entity — don't draw it twice. Use role labels on the two lines instead
- ⚠️ Don't confuse COMMANDS (1:N, exactly one captain per flight) with STAFFS (M:N, multiple cabin crew)
- ⚠️ Seat number belongs on RESERVATION — not on FLIGHT or PASSENGER — it's specific to a booking
- ⚠️ Don't forget: PILOT is an IS-A specialisation of EMPLOYEE, inheriting EmployeeID and Name
    </details>
</details>

#### Self Assessment — How did your diagram compare?

- [x] I drew AIRPORT only once but used role labels for departure/arrival
- [x] I drew RESERVATION as a weak entity with a double rectangle
- [x] I drew IS-A hierarchy for PILOT and CABIN_CREW under EMPLOYEE
- [x] I correctly assigned COMMANDS as 1:N and STAFFS as M:N
- [x] I placed SeatNumber on RESERVATION, not on FLIGHT or PASSENGER