# Database System Architecture
Content from Neso [Academy]https://www.youtube.com/watch?v=OMwgGL3lHlI&list=PLBlnK6fEyqRiyryTrbKHX1Sh9luYI0dhX&ab_channel=NesoAcademy
![image](https://user-images.githubusercontent.com/83261924/218288730-c47a3a8d-b8fe-40e7-94ec-c066b64caa53.png)


* RDBMS
* Relational Database
* Database Design & E-R Model
* SQL
* 

Database Management System
![image](https://user-images.githubusercontent.com/83261924/218282848-e2fe033b-0bad-4c37-a357-6e79be4f5807.png)

## Storage Manager
* Low level data stored -Storage Manager - Application Programs.
* Queries submitted to the system
* Interection with file manager
* raw data are stored on the disk using file system provided by OS
* Translates various DML statements into low-level file system commands
* Responsible for storing,retreiving and updating data

### The Storage Manager
* Authorization and integrity manager - user auth, data integrity
* transactions manager - ensure data are not conflict.
* file manager - allocating space for data in disk / data structure
* buffer manager - doing query.

### Data Structures
* Data files - where data are located in disk
* Data dictionary - metadata(store data about data)
* indices - help retreive data faster. (index pages)

### Transaction Management
* recovery manager - recover failure state
* concurrency-control manager

Transaction is one logical operation.
* Atomicity requirement - All or None
* Consistency
* Durability - withstand failure, incase some transaction missing when this accur


## Query Processor
(Data Manupulation Language) DML Query - for change database data
(Data Definition Language) DDL Interpreter - full previledge over database. add column...
DML compiler and organizer - 
application program object code - will convert 

### Query Evaluation Engine


---
## DBMS Language - SQL
