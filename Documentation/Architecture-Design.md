**Vertex Architecture**
*Designed and written by Lewis Stuart*

This wiki page defines the initial architecture for the webserver, which includes the following components:
1. Technologies used- this defines all imported modules and technologies that will be used for the development of the system
2. Database design- All table classes and subsequent relations
3. File structure (and consequently components of system)

***1)Technologies used:***

The following technologies are essential for the creation, management and development of our web solution
*  SQLite- database language
*  Flask- a lightweight webserver framework that handles HTTP requests by executing functions depending on the specified URL
*  SqlAlchemy with ORM- used for mapping Python classes to database tables, with objects referring to rows in that table
*  Jinja2- allows data to be passed and formatted in normal HTML files
*  Passlib/Hashlib- used for hashing and encrypting passwords
*  PyTest- testing framework for ensuring that the webserver is executing effectively
*  Alembic- used for database migrations and ensuring SqlAlchemy classes are synced with the tables in the database
*  NGinx/uWSGI- software used for deploying the final webserver on a Linux system
*  SSL- provides secure connection between clients and the webserver
*  PyCharm- IDE used for individual development of the webserver

***2)Database design:***

*Database schema* (does not contain all fields that will be implemented):
Format:
Bold = Primary key
Italic = Foreign key
| | = Dependent on another table field

Account component:

1) User(**User_ID**, Email, Password, Card_details,...)

2) Customer(**Customer_ID**, *User_ID*,...)

3) Employee(**Employee_ID**, *User_ID*, |Composite_Role|)

4) Manager(**Manager_ID**, *User_ID*,...)

Activity component:

5) ActivityType(**Activity_Type_ID**, Name, Description, Tags, Category, Minimum_Age, Maximum_Activity_Capacity, Hourly_Activity_Cost, Hourly_Activity_Price, |Valid_Composite_Roles|, Max_Staff, Min_Staff, Leisure_Center_Run)

6) Activity(**Activity_ID**, *Activity_Type_ID*, *Facility_ID*, Start_DateTime, End_DateTime)

Employee/Manager data component:

7) Router(*Employee_ID*, *Activity_ID*, *Role_id*)

8) Facility(**Facility_ID**, Name, Description, Max_Capacity)

9) Role(**Role_ID**, Role_Name, Description, Hourly_Pay)

Transaction component:

10) Receipt(**Receipt_ID**, *Customer_ID*, Total_Cost, Creation_Time)

11) Booking(**Booking_ID**, *Activity_ID*, *Receipt_ID*)

12) Subscription(**Subscription_ID**, *Activity_Type_ID*, Start_Date, End_Date, Receipt_ID)

13) Membership(**Membership_ID**, *Membership_Type_ID*, Start_Date, End_Date, Receipt_ID)

14) MembershipType(**Membership_Type_ID**, Name, Description, Discount, Monthly_Price)

Total: 14 Tables 

Explanation:

1) User- Holds all data related to all users of the website, this includes customers, employees and managers. User_ID, which is the primary key of this table, is referenced in all of the sub-tables such that all roles can access their user data. Fields stored in this table includes items such as: first name, last name, DOB, ext... (Basically all attributes needed for all users of the website)

2) Customer- Contains all attributes which are only used by customers and only contains the User_ID of a customer type. This
table is referenced in the receipts, as customers can participate in booking transactions, subscriptions and memberships

3) Employee- Contains all attributes related only to employees. Employees can edit certain parts of the websites (depending on their roles) The most important of this is a composite role field, which contains a numeric string that refers to all roles that that employee can partake in with certain activities (For example- an employee may be allowed to take the role of a lifeguard, as well as being a activity leader, for a specific activity), the
roles that the employee has taken can be inferred from this string value. This works by converting the string value into an
integer in base 2 (binary representation), and having each 1 or 0 being a Boolean value that dictates whether that employee
has a specific role, based on the reverse order of the roles stored in the role table. For example-
An employee has the composite role value of 10, in the role table is the following records:

| Role_ID | Name | Description | Hourly_Pay |
| ------ | ------ | ------ | ------ |
| 1 | Party Host | ... | ... | 
| 2 | Gym Helper | ... | ... | 
| 3 | Personal Trainer | ... | ... | 
| 4 | Lifeguard  | ... | ... |

(The description and hourly pay have been left blank as they are not important)
Extracting this data in order based on primary key the following roles are returned:
Lifeguard - Gym Helper - Personal Trainer - Party Host

Converting the composite role value into a binary representation gives:
1 0 1 0

Hence by comparing the ordering, the following is deduced about that employee's roles:
*  They are not a Gym Helper or a Lifeguard
*  They can take up the role of Personal Trainer or Party Host

The reason for this is that certain activities require certain roles, and only employees that are qualified for that role can
be assigned to partake in that activity (eg. an activity by the pool requires a lifeguard)

4) Manager- contains all data related to managers of the website- these accounts have access to edit almost anything on the database.

5) Activity type- refers to a certain activity that is hosted in the leisure center. An activity type could be anything from 'general swim' to 'trampolining'. These activity types can be added by managers. Instances of activity types are referenced in the activity table. Activity types have the following fields:
*  Name- name of the activity (eg. 'Football')
*  Description- description of the activity (eg. 'Football is a highly popular sport played by all ages...'), this will be displayed on the website when a user views an individual activity page
*  Tags- a colon separated list of all tags related to the activity (eg. 'high-energy:all-ages:popular')
*  Category- a defined category for that activity, this will be used for filtering activities when the user searches for an activity of a specific category (eg. "Ball-Sport")
*  Minimum_Age- the minimum age that a customer needs to be to take part in this particular activity (eg. 16+)
*  Max_Activity_Capacity- the max amount of customers that can attend an activity
*  Hourly_Activity_Cost- the hourly cost of hosting that activity (eg. £2 an hour)
*  Hourly_Activity_Price- the hourly rate that is charged from a customer for that activity (eg. £10 an hour to attend)
*  Valid_Composite_Roles- uses the same formula as for determining the employee roles. This attribute is a numerical string that relates to a list of roles. In this context, the roles refer to which roles are needed for that activity (eg. a leader and a helper is needed to run a football activity)
*  Max_Staff- maximum amount of staff that can partake in an activity (eg. no more than 3 staff for a football activity)
*  Min_Staff- minimum amount of staff needed to run an activity (eg. must be at least 2 staff for a football activity)
*  Leisure_Center_Run- a Boolean value that states whether the leisure center runs the activity (or if it would be run by an external club or society), if so, then the user can can get discounts on the activity if they have a membership, otherwise they will have to purchase an individual subscription if they want to get discounts on this activity (eg. Football is not run by the leisure center but general swim is)

6) Activity- used for creating individual instances of activities (what activities are occurring and at what time). This is what is used for creating the timetabling system, the following fields will explain how this works:
*  Activity_Type_ID- the activity that is being run, this relates to the record in the activity type table (eg. a football activity is happening)
*  Facility_ID- the facility that the activity is hosted in, this refers to individual facility instances in the facility table (eg. this football activity is happening in sports hall 2)
*  Start_DateTime- the date and time that the activity is happening (eg. Tuesday at 16:00)
*  End_DateTime- the date and time that the activity finishes (eg. Tuesday at 15:30)
There will be triggers in place to ensure that all start and end times are valid (eg. not on two different days, not outside of when the leisure center is shut, ext...). This table holds data for all the activities that are happening and when they are happening

7) Router- this refers to which staff are taking part in which activity, and what role they will be partaking for each activity, the fields include
*  Employee_ID- which employee is taking part in an activity (eg. employee with id 2)
*  Activity_ID- the activity that is taking place (eg. football between 2:00 and 4:00), this relates to the activity table
*  Role_id- the id of the role they will partake (eg. role id 4, which could be a lifeguard)

8) Facility- refers to all the facilities that are offered by the leisure center, as well as their maximum capacity. This maximum capacity must be greater than or equal to the number of customers that are attending an activity that is taking place at that facility (eg. sports hall 2, which has a maximum capacity of 70 people)

9) Role- contains all the roles that an employee can have in the leisure center, as well as the hourly pay they will receive for taking that role (eg. a leader role which has an hourly pay of £12.00). The order of the records (in order of ID) cannot change the composite role values depend on this order being the consistent; fortunately adding new roles will not effect the composite roles, whereas deleting a role will

10) Receipt- holds all the data that is needed for a receipt; the beauty of having a separate table for receipts is that: memberships, booking and subscriptions (from here on when I refer to a transaction, I am referring to these three operations) all use the same receipts, and thus a foreign receipt ID is included which refers to an individual receipt record. This also allows for multiple bookings in one session to take place (eg. adding items to a basket) to occur. Hence the receipt has the following fields:
*  Customer_ID- the ID of the customer who made a transaction (eg. customer with id 1 made a transaction)
*  Total_Cost- the total cost of the entire transaction (eg. this cost £32.50)
*  Creation_Time- when the transaction occurred (eg. 10:11 on the 4/01/2019)
This receipt can also be used for creating a QR code and thus can be used for refunding/canceling a transaction

11) Booking- refers to when a customer books an activity, this is extremely simple and just contains the activity that the customer has booked, and the receipt of the transaction (eg. customer with ID 2 booked to attend activity with ID 506, which is football in sports hall 2 on Tuesday between 2:00 and 4:00)

12) Subscription- a subscription in this context refers to when a user pays a annual or biannual fee that allows them to attend a specific activity for free (eg. Customer with ID 2 purchased a subscription to football for 6 months, meaning they will not be charged for booking to attend a football activity). This is why the Activity Type ID is referenced rather than individual Activity IDs. Start and End date refers to the duration that this subscription is valid for

13) Membership- a membership in this context refers to memberships offered by the leisure center, allowing that user to access the leisure center facilities at a discounted rate. There are different tiers of memberships that allow for different amounts of discount to be applied, these are defined by the Membership_Type_ID (eg. Customer with ID 2 bought a standard membership, allowing them to get 30% off all usage of leisure center facilities). If the customer has the highest tier then they will get all leisure run activities for free, and they will not need to book to attend; they will be let in if there is space

14) MembershipType- A lookup table containing all the membership types, the monthly price of a customer purchasing them and the discount percentage (eg. a standard membership costs £15 a month and provides 40% off all leisure run activities) 

[Credit to Jasmine and Chan who assisted me with the development of this database schema]

***3)File Structure***

For the webserver, the following file structure has been chosen as I believe it has clear separation between the different layers of the server; this file structure means that a 4-tier architecture can be deployed:
1. Application- the individual HTML/Jinja2 templates
2. Views- this configures requests and renders the correct template with the correct data
3. Data transactions- files that contain functions that deal with data transfer between the views and database
4. Database

The file structure image is attached to this wiki, study this before proceeding with the explanation:
![FileStruct](uploads/a10896d49b666070b818aafb139e7c5a/FileStruct.png)

Explanation:

1) *TheVertex*- the main root file for the entire server

2) *Alembic*- contains all data related to running alembic

3) *Logs*- contains two log files:
*  **Server_Error.log**- stores all the errors that occur in flask
*  **Transaction.log**- stores information about all transactions between the views and the database; basically keeps track of all data transfer in or out of the database through the server

4) *Server*- holds all scripts needed for if the website was to be deployed on a Linux server running uWSGi and NGINX

5) *Tests*- contains all PyTest scripts used for manually testing the webserver and checking for regression errors

6) *Main*- contains all source files which are needed for when the server is running

7) *Data*- designed to store all python script files related to the database (but not including the database itself)

8) **Db_session.py**- a script that is used to configure the database and is used for creating a session that can communicate with the database; this can be done by including the file and returning a session using the create_session() function

9) *db_classes*- 4 components that were discussed in the database section, which contain all the SQLAlchemy classes for managing the tables for the database

10) *Transactions*- contains scripts which manage the transactions of data in and out of the database through controlled functions. These scripts are split into the 4 database components. The important part of using this architecture is that data transfer between the views and database is done through these scripts, meaning detecting errors and managing data flow is much simpler. All of these scripts contain functions that are called upon in the individual views, an example of a function in one of these scripts could be 'return_customer_with_id(int: id)'- this also allows for validation to occur in these functions and allows tighter control over what data is allows to enter or leave the database

11) *DB* - contains the actual SQLite database file

12) *Static*- contains all static files used in the website, this includes the following sub-folders:
*  Css- contains all Css files. The most important of which is a Css file which is defined as 'main.css'; this has the property where all Css changes made in this file will impact every webpage on the website, this is beneficial for setting things like default fonts or backgrounds, ext...
*  Fonts- includes any .tff font files that need to be referenced in Css files 
*  Imgs- contains all images that are used by the website
*  Js- contains any JavaScript files that are used on the website. Similarly to the Css folder, there is a JavaScript file called 'main.jss', where all changes to this file will effect all of the webpages; this is beneficial for systems such as accepting cookies
There is also a Favicon file which is included on all the webpages

13) *Templates*- holds all of the HTML files that are used on the website (these HTML files are used by views to render specific templates containing specific data depending on which webpage and data the user is accessing). In this templates folder contains a series of sub-folders which consist of the main components of the website which each hold templates for:
*  Account- account creation, login or managing (eg. login)
*  Activities- activity viewing or management (eg. timetabling)
*  Transactions- related to bookings, subscriptions or membership management
*  Includes (explained below)
*  Index- index or similar pages
*  Info- providing information (eg. company description page)
*  Misc- unique pages not related to any of the above changes (eg. help page, policy page)

14) **_Main_Layout.html**- inside of the includes folder is this file, which is the most important template on the server. This allows for a standard format to be implemented, and data in this file is included in all templates. Rather than having to define the same data repetitively for every template file (eg. tags in the head section), this template will include all of these tags already and thus allow for other templates to define the data that is unique to that page. This also allows for consistent navigation and footers to be defined, which can be included depending or not included depending on their Boolean value that is passed to the template. Finally, scripts such as Bootstrap and JQuery are referenced once in this file, and thus will be included in all other templates and do not need to be referenced again. 

This is done by defining blocks, which data can be inserted into from other templates, the blocks defined in this file are as follows:
*  Title- when referenced allows templates to easily set a title for the template
*  Additional_Css- allows for Css to be easily linked in the header file
*  Additional_Js- allows for JavaScript to be easily referenced
*  Main_content- this is where all of the main html/jinja2 will be included, this ensure that it is after the head and navigation section but before the footer section

This file also has some conditions that allow for certain sections to be included depending on the Boolean value passed to the template:
*  Nav- if this variable is set to true, then the navigation section included in the main_layout file will be included in the final render of the template
*  Footer- similarly, if this is set to true then the footer will be included

All template files should extend from this default template

15) *Views*- these contain view scripts, which are split into the same sections as that of the templates. Views have the responsibility of deciding which functions to execute depending on what URL is sent to the server. Due to the file structure that has been implemented, these views can only interact with the database through the database transaction files. These views can analyse cookie and post/get data to decide what data to include, and then render the appropriate template

16) **App.py**- this is the main script which has the purpose of running the server, this has the following responsibilities:
*Creating a flask instance which will run the server
*Register blueprints- this connects all the views to the flask app
*Set up the database and creates it if it does not exist
*Creates a system for logging data
*Defines pages to be displayed for if a page does not exist for a URL or if the server encounters an error while rendering a page
*Starts the flask app

It is important to note that this architecture will change overtime as more functionality is added, however I believe this is a good starting point

 
