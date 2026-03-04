# Database Normalization

Database normalization is the process of organizing data in a database to reduce redundancy and improve data integrity.

It involves dividing large tables into smaller tables and defining relationships between them.

---

# Why Normalization is Important

Normalization helps to:

- Reduce **data redundancy**
- Avoid **update anomalies**
- Maintain **data consistency**
- Improve **database design**
- Make queries and updates more reliable

---

# 1NF (First Normal Form)

### Rule
A table is in **First Normal Form (1NF)** if:

- Each column contains **atomic (indivisible) values**
- No **repeating groups**
- Each record can be uniquely identified by a **primary key**

### Example (Not in 1NF)

| StudentID | Name | Subjects |
|----------|------|---------|
| 1 | Raj | DBMS, OS |
| 2 | Amit | CN, DBMS |

Problem: Multiple values stored in a single column.

### Convert to 1NF

| StudentID | Name | Subject |
|----------|------|--------|
| 1 | Raj | DBMS |
| 1 | Raj | OS |
| 2 | Amit | CN |
| 2 | Amit | DBMS |

---

# 2NF (Second Normal Form)

### Rule

A table is in **2NF** if:

1. It is already in **1NF**
2. Every **non-key attribute is fully dependent on the entire primary key**

This mainly applies when we have a **composite primary key**.

### Example (Not in 2NF)

| StudentID | CourseID | StudentName | CourseName |
|----------|----------|------------|------------|

Primary Key: `(StudentID, CourseID)`

Dependencies:


StudentID → StudentName
CourseID → CourseName
(StudentID, CourseID) → other attributes


Problem: Attributes depend only on **part of the key**.

### Convert to 2NF

**Students Table**

| StudentID | StudentName |

**Courses Table**

| CourseID | CourseName |

**Enrollment Table**

| StudentID | CourseID |

---

# 3NF (Third Normal Form)

### Rule

A table is in **3NF** if:

1. It is in **2NF**
2. There are **no transitive dependencies**

Meaning:

> Non-key attributes should depend **only on the primary key**, not on other non-key attributes.

---

### Example (Not in 3NF)

| StudentID | StudentName | AdvisorID | AdvisorOffice |
|----------|-------------|-----------|---------------|

Dependencies:


StudentID → StudentName
StudentID → AdvisorID
AdvisorID → AdvisorOffice


Here:


StudentID → AdvisorID → AdvisorOffice


This is **transitive dependency**.

---

### Convert to 3NF

**Students Table**

| StudentID | StudentName | AdvisorID |

**Advisors Table**

| AdvisorID | AdvisorOffice |

Now every non-key attribute depends **directly on the primary key**.

---

# BCNF (Boyce-Codd Normal Form)

BCNF is a **stronger version of 3NF**.

### Rule

For every functional dependency:


A → B


**A must be a super key.**

Meaning: The attribute determining another attribute must uniquely identify rows.

---

# BCNF Example

### Table

| Student | Subject | Teacher |
|--------|--------|--------|
| Raj | DBMS | Prof A |
| Raj | OS | Prof B |
| Amit | DBMS | Prof A |
| Neha | OS | Prof B |

### Functional Dependencies


(Student, Subject) → Teacher
Subject → Teacher


Candidate Key:


(Student, Subject)


Problem:


Subject → Teacher


But **Subject is not a super key**, which violates BCNF.

---

# Convert to BCNF

Split the table.

### StudentSubject Table

| Student | Subject |

Primary Key:


(Student, Subject)


### SubjectTeacher Table

| Subject | Teacher |

Primary Key:


Subject


Now every dependency has a **super key determinant**, so the schema is in **BCNF**.

---

# Quick Summary

| Normal Form | Rule |
|-------------|------|
| 1NF | Atomic values, no repeating groups |
| 2NF | No partial dependency |
| 3NF | No transitive dependency |
| BCNF | Every determinant must be a super key |

---

# Key Interview Tip

A quick way to remember:
