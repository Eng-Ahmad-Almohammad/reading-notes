# Database Normalization 
## Introduction
### Database normalization is a process used to organize a database into tables and columns.  The main idea with this is that a table should be about a specific topic and only supporting topics included. Take a spreadsheet containing the information as an example, where the data contains salespeople and customers serving several purposes:
- Identify salespeople in your organization

- List all customers your company calls upon to sell a product

- Identify which salespeople call on specific customers.

### By limiting a table to one purpose you reduce the number of duplicate data contained within your database. This eliminates some issues stemming from database modifications.


### There are three normal forms most databases adhere to using.  As tables satisfy each successive database normalization form, they become less prone to database modification anomalies and more focused toward a sole purpose or topic. Before we move on be sure you understand the definition of a database table.

## Reasons for Database Normalization

### There are three main reasons to normalize a database.  The first is to minimize duplicate data, the second is to minimize or avoid data modification issues, and the third is to simplify queries. 

## Data Duplication and Modification Anomalies

### Duplicated information presents two problems:

- It increases storage and decrease performance.

- It becomes more difficult to maintain data changes.

## Insert Anomaly

### There are facts we cannot record until we know information for the entire row.

## Search and Sort Issues
### The last reason we’ll consider is making it easier to search and sort your data.


## Definition of Database Normalization

### There are three common forms of database normalization: 1st, 2nd, and 3rd normal form. They are also abbreviated as 1NF, 2NF, and 3NF respectively. 

### The forms are progressive, meaning that to qualify for 3rd normal form a table must first satisfy the rules for 2nd normal form, and 2nd normal form must adhere to those for 1st normal form. Before we discuss the various forms and rules in detail, let’s summarize the various forms:

1- *First Normal Form*: The information is stored in a relational table with each column containing atomic values. There are no repeating groups of columns.


2- *Second Normal Form*: The table is in first normal form and all the columns depend on the table’s primary key.


3- *Third Normal Form*: the table is in second normal form and all of its columns are not transitively dependent on the primary key.

