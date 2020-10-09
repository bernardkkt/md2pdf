<DIV class="markdown-body" style="font-size: 1.25em;">

# Designing a Database

## Introduction

In database design, developers will start with **gathering requirements** from customers, then proceed to **conceptual design**, **logical design** and lastly, **physical design**. This article covers all these topics **except physical design**.

## Key Concepts/Glossary

<figure class="image"><img src="./assets/entrel-view.svg" alt="Entity Relationship">
  <figcaption style="text-align: center; font-style: italic;">Entity Relationship Diagram</figcaption>
</figure>

<figure class="image"><img src="./assets/table-view.svg" alt="Table">
  <figcaption style="text-align: center; font-style: italic;">Components of a database table</figcaption>
</figure>

|                   Name | Definition                                                                                                                |
|-----------------------:|:--------------------------------------------------------------------------------------------------------------------------|
|                 Entity | a real-world object such as an employee or a project                                                                      |
|           Relationship | an association among entities                                                                                             |
|       Relational model | where data is represented as tables (also known as *relations*)                                                           |
|    Table/Relation/File | a subset of the Cartesian product of a list of domains characterized by a name                                            |
| Column/Attribute/Field | name/property that describes an entity                                                                                    |
|       Row/Tuple/Record | a group of data values corresponding to the attributes                                                                    |
|                 Domain | a set of acceptable values that a column is allowed to contain                                                            |
|                 Degree | number of attributes in a table                                                                                           |
|            Cardinality | number of unique (non-repeating) rows in a table                                                                          |
|                    Key | an attribute or a group of attributes whose values can be used to uniquely identify an individual entity in an entity set |
|            Primary key | a key which is is unique and minimal, chosen to be used as an identifying mechanism for the whole entity set              |
|            Foreign key | an attribute in a table that references the primary key in another table                                                  |
|          Composite key | two or more attributes which can be used to uniquely identify each record in a table                                      |

<DIV style="page-break-inside: avoid;">

## Overview

![Flow chart](./assets/design-view.svg)

</div>

## Identifying Requirements

Since there is no more retrievable information other than the descriptions and instructions from the question paper, students need to temporarily switch their role as a developer to a user of the database system they are going to design. This will help students to understand the expectation of their work from a customer’s perspective. This method relatively consumes shorter time compared to other fact-finding techniques.

The first thing students should do would be **looking up similar DBMS** on the internet. Almost a certainty students are able to find a system that works similarly, if not a complete suite. The system could be in a form of a file meant to be opened with a database management software (*e.g. Microsoft Access*), or a project repository that contains source code of the DBMS. If students are able to find one, they have to access and interact with the system as a user. Doing so will help students to **identify entities, attributes and relationships** that should be included in their database design.

In case of a fruitless search, students can still utilise their imaginations to draw out their design on a piece of paper (or more). After all, the objective is to let student identify entities, attributes and relationships through visualisation.

<DIV style="page-break-inside: avoid;">

### Building a Picture

Typically, a user login page is a good place to begin with. The sketches should include elements (such as input forms and buttons) corresponding to the pages navigated according to users’ interaction. Students are free to exercise their creativity as long as they are mindful of a few general rules:

1.  Keep the content concise in each page, focus on meaningful interaction relevant to the topic only. (*e.g. there is **no need to create a user sign-up page** if it is not required*)
2.  Check for redundant/unnecessary collection of information in all input forms. (*e.g. instead of first/last name, **asking for full name is enough** if there is no requirement to identify surname*)
3.  Collection of data should lead to a record at database.
4.  Examine the logic behind the interaction and how it affects the subsequent pages.

</div>

## Forming a Master Table

The steps below show how a master table can be derived from the last section:

1.  Construct an entity relationship diagram for each relation that brings 2 entities together (*refer to the first diagram above*).
2.  Attempt to create one single table that includes **all** attributes.
    1.  Fill in all the attributes into the table header
    2.  Add records (rows) to the table. The data can be random in nature, but make sure all entries are sensible representations of actual scenarios.
3.  Give an appropriate entity name for the table you have created so far.

In an event where creating a single master table does not make sense (*e.g. groups of entities that do not relate to each other in any way based on the entity relationship diagrams*), create a table for each of the group while strictly following step 2 and step 3 above.

## Normalisation

Students will need to split the large table into several normal forms, a process known as normalisation. Below is an example of an unnormalised form resembles a master table:

<DIV style="font-size: 0.8em;">

| StudentNo |   StudentName   |      Major      | CourseNo | CourseName | InstructorNo |  InstructorName   | InstructorLocation | Grade |
|:---------:|:---------------:|:---------------:|:--------:|:----------:|:------------:|:-----------------:|:------------------:|:-----:|
|  S73621   | Abraham Snodden | Human Resources |  55586   |   Arabic   |   G649227    |   Ernest Disdel   |         NY         |   A   |
|  S73621   | Abraham Snodden | Human Resources |  58499   |  Russian   |   G126077    | Sigfried McGiffie |         OH         |   C   |
|  S73621   | Abraham Snodden | Human Resources |  63009   |   German   |   G725957    |   Ginni Chesnut   |         TX         |   C   |
|  S73262   |   Symon Trowl   |   Accounting    |  58499   |  Russian   |   G126077    | Sigfried McGiffie |         OH         |   B   |
|  S73262   |   Symon Trowl   |   Accounting    |  63009   |   German   |   G725957    |   Ginni Chesnut   |         TX         |   B   |
|  S75343   | Wynnie Larking  |   Accounting    |  55586   |   Arabic   |   G649227    |   Ernest Disdel   |         NY         |   C   |

Follow the remaining sections to see how it can be normalised (up to 3<sup>rd</sup> normal form).

</div>

<DIV style="page-break-inside: avoid;">

### First Normal Form (1NF)

The first normal form requires the table to contain only a single value anywhere in the cells, and there should be no repeating groups throughout the rows.

<div style="padding: 0; display: table-cell; text-align: center; vertical-align: middle;">
    <img src="./assets/multi-val.svg" alt="Multiple Value">
    <img src="./assets/rep-group.svg" alt="Repeating Group">
</div>

The examples above have nothing look alike with the unnormalised table, but still it has not yet fulfil the criterion for 1NF. Read the table carefully and you will notice the columns after “**Major**” are the repeating group (*i.e. each student gets a grade for each course the student has taken, and each student can take multiple courses*).

Here are the steps to normalise the table to 1NF:

1.  Identify the repeating group(s).
2.  Create a new table by detaching the repeating group from the old table.
3.  Identify the primary key for all tables.
4.  Form composite keys to retain the relationship between tables if necessary.

| Before Normalisation                                                                                                                      |
|:------------------------------------------------------------------------------------------------------------------------------------------|
| **Student\_Grade\_Report** (StudentNo, StudentName, Major, CourseNo, CourseName, InstructorNo, InstructorName, InstructorLocation, Grade) |

| After Normalisation (1NF)                                                                                                                                                                      |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Student** (<ins>StudentNo</ins>, StudentName, Major) <br> **StudentCourse** (<ins>StudentNo</ins>, <ins>CourseNo</ins>, CourseName, InstructorNo, InstructorName, InstructorLocation, Grade) |

</div>

### Second Normal Form (2NF)

The second normal form requires each non-key attribute in a table to be completely dependent on whatever primary/composite keys exist in the table. If there is only one primary key in a 1NF table, then it can be considered as a 2NF table.

**Important: The table must already in 1NF before it can be normalised to 2NF.**

Here are the steps to normalise 1NF to 2NF:

1.  Examine all non-key attributes and their dependencies with the primary/composite key in the table.
2.  Form a new table by detaching all non-key attributes with incomplete dependencies.
3.  Create or appoint a primary/composite key for the new table.

| Before Normalisation (2NF)                                                                                                                                                                     |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Student** (<ins>StudentNo</ins>, StudentName, Major) <br> **StudentCourse** (<ins>StudentNo</ins>, <ins>CourseNo</ins>, CourseName, InstructorNo, InstructorName, InstructorLocation, Grade) |

| After Normalisation (2NF)                                                                                                                                                                                                                    |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Student** (<ins>StudentNo</ins>, StudentName, Major) <br> **CourseGrade** (<ins>StudentNo</ins>, <ins>CourseNo</ins>, Grade) <br> **CourseInstructor** (<ins>CourseNo</ins>, CourseName, InstructorNo, InstructorName, InstructorLocation) |

### Third Normal Form (3NF)

The third normal form requires no transitive dependencies in a 2NF table. In another words, there should not be any functional dependencies among the non-key attributes in the table.

**Important: The table must already in 2NF before it can be normalised to 3NF.**

Here are the steps to normalise 2NF to 3NF:

1.  Examine all non-key attributes and their dependencies with each other in the table.
2.  Create a new table by detaching all dependent attributes from the table.
3.  Repeat Step 1 and Step 2 until no more inappropriate dependencies in the table(s).

| Before Normalisation (3NF)                                                                                                                                                                                                                   |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Student** (<ins>StudentNo</ins>, StudentName, Major) <br> **CourseGrade** (<ins>StudentNo</ins>, <ins>CourseNo</ins>, Grade) <br> **CourseInstructor** (<ins>CourseNo</ins>, CourseName, InstructorNo, InstructorName, InstructorLocation) |

| After Normalisation (3NF)                                                                                                                                                                                                                                                        |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Student** (<ins>StudentNo</ins>, StudentName, Major) <br> **CourseGrade** (<ins>StudentNo</ins>, <ins>CourseNo</ins>, Grade) <br> **Course** (<ins>CourseNo</ins>, CourseName, InstructorNo) <br> **Instructor** (<ins>InstructorNo</ins>, InstructorName, InstructorLocation) |

<DIV style="page-break-inside: avoid;">

## Construction of ER Diagram

Populating the tables and labelling the relationships among them form an ER diagram. After 3 rounds of normalisation, there is only one step away to constructing the ER diagram. Without figuring out the relationships among the entities (tables), it is impossible to construct a complete ER diagram. In order to construct one for the example above, the following assumptions have to be made:

-   A student can take multiple courses and receive grades respectively.
-   It is possible that a student may not be taking any courses.
-   Each course will always have one instructor assigned to it.
-   Not all instructors are assigned to a course.
-   It is possible that a course has no students enrolled in it.

All these information can be compiled into the following ER diagram:

![ER Diagram](./assets/erd.svg)

</div>

<DIV style="page-break-inside: avoid;">

## Credits

This article contains work from the following source: 

1.  Watt, A. and N. Eng. (2014). Database Design – 2nd Edition. Victoria, B.C.: BCcampus. Retrieved from https://opentextbc.ca/dbdesign01/

</div>

</div>
