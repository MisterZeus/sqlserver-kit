# SQL Server Management Studio Tips


## SSMS Shortcuts
All shortcuts you can find [here]()
Most useful 


## Set Keyboard Shortcuts for Favorite Stored Procedures


## Selecting a block of text using the ALT Key
By holding down the ALT key as you select a block of text you can control the width of the selection region as well as the number of rows.


## Script Table and Column Names by Dragging from Object Explorer
Save keystrokes by dragging
Drag the ‘Columns’ folder for a table in to auto-type all column names in the table in a single line.
- Warning: this doesn’t include [brackets] around the column names, so if your columns contain spaces or special characters at the beginning, this shortcut isn’t for you
 -  Dragging the table name over will auto-type the schema and table name, with brackets.


## Disable Copy of Empty Text
<a id="disable-copy-of-empty-text"></a>

 - Select a block of text to copy;
 - Move the cursor the place where you want to paste the code;
 - Accidentally press `Ctrl+C` again instead of `Ctrl+V`;
 - Block of copied text is replaced by an empty block;

This behavior can be disabled in SSMS: go to Tools > Options > Text Editor > All Languages > General > ‘Apply Cut or Copy Commands to blank lines when there is no selection’ and uncheck the checkbox.


## Client Statistics
When you enable that option for your session, SQL Server Management Studio will give you more information about the client side processing of your query.

The Network Statistics shows you the following information:
 - Number of Server Roundtrips
 - TDS Packets sent from Client
 - TDS Packets received from Server
 - Bytes sent from Client
 - Bytes received from Server

The Time Statistics additionally shows you the following information:
 - Client Processing Time
 - Total Execution Time
 - Wait Time on Server Replies


## Moving columns in the results pane
It may not be immediately obvious but you can switch columns around in the results pane when using the grid view, by dragging the column headers and dropping them next to another column header.
This can be useful if you want to rearrange how the results are displayed without amending the query, especially if you have a lot of columns in your resultset.


## Using GO X to Execute a Batch or Statement Multiple Times
The `GO` command marks the end of a batch of statements that should be sent to SQL Server for processing, and then compiled into a single execution plan. 
By specifying a number after the ‘GO’ the batch can be run specified number of times. This can be useful if, for instance, you want to create test data by running an insert statement a number of times. Note that this is not a Transact SQL statement and will only work in Management Studio (and also SQLCMD or OSQL). For instance the following SQL can be run in SSMS :

```sql
CREATE TABLE TestData(ID INT IDENTITY (1,1), CreatedDate DATETIME)
GO

INSERT INTO TestData(CreatedDate) SELECT GetDate()
GO 10
```

This will run the insert statement 10 times and therefore insert 10 rows into the TestData table.
In this case this is a simpler alternative than creating a cursor or while loop. 


## SSMS Template Replacement
One under-used feature of Management Studio is the template replacement feature. SSMS comes with a library of templates, but you can also make your own templates for reusable scripts.

In your saved .sql script, just use the magic incantation to denote the parameters for replacement. The format is simple: `<label, datatype, default value>`

Then, when you open the .sql script, you hit CTRL + Shift + M, and SSMS will give you a pop-up to enter your replacement values


## Color coding of connections
SQL Server Management Studio has the capability of coloring the bar at the bottom of each query window, with the color dependent on which server is connected.
This can be useful in order to provide a visual check of the server that a query is to be run against, for instance to color code production instances as red, development as green and amber as test.
This can also be used in conjunction with Registered Servers and CMS (Central Management Server).
To add a color bar when connecting to the server click on the Options button in the Connect to Database Engine window and then select the Connection Properties window.
Select the check box towards the bottom of the window and use the ‘Select…’ button to choose a color.


## SQLCMD mode
Switching on SQLCMD mode enables a number of useful extra scripting style commands in SSMS.In particular you can use it to change to the connection credentials within the query window, so that you can run a query against multiple servers from the same query window.
There are more details of how to do this here: [Changing the SQL Server connection within an SSMS Query Windows using SQLCMD Mode](http://www.sqlmatters.com/Articles/Changing%20the%20SQL%20Server%20connection%20within%20an%20SSMS%20Query%20Windows%20using%20SQLCMD%20Mode.aspx)


## Script multiple objects using the Object Explorer Details Windows
Individual database objects, such as a table or stored procedure, can be scripted within SSMS by right clicking on the object within Object Explorer and selecting the appropriate item in the drop down menu.
However if you have a lot of objects to script that can quickly become time consuming.
Fortunately it’s possible to select multiple objects and script them up all together in a single query window.
To do this just open the Object Explorer Details window from the View menu (or press the F7 key).
If you want to script up multiple (or all) tables, select the Tables item under the relevant database in Object Explorer.
A list of all tables appears in the Object Explorer Details window.
Select the tables you want to script (using the Control key if necessary) and then right click and select which script option you want – e.g. to create a table create script for all tables


## Registered Servers / Central Management Server
If you have a lot of servers then re-entering the details in Object Explorer every time you start SSMS can be frustrating and time consuming.
Fortunately there are two facilities within SSMS that enable these details to be entered just once and “remembered” each time you open up SSMS.
These two facilities are Registered Servers and Central Management Servers.
These were introduced in different versions of SQL Server and work in different ways, each has its own advantages and disadvantages so you may want to use both.

To add a registered server open the Registered Servers window from the View menu (or click CTRL + ALT + G), the window should appear in the top left corner of SSMS.
Right click on the Local Server Groups folder and select ‘New Server Registration…’. Enter the server details and close the window.
This new server should then appear under Local Server Groups, you can then right click and open up the server in Object Explorer or open a new query window.
The server details are stored locally in an XML file and so will appear next time you open SSMS.
If you have a lot of servers then you can also create Server Groups to group together similar servers.
One advantage of creating groups (other than being able to logically group similar servers together) is that you can run a query against all servers in the group, by right clicking the group and selecting ‘New Group’.

Central Management Server are similar to Registered Servers but with some differences, the main one being that the server details are stored in a database (the Central Management Server) rather than a local file.
A significant limitation with CMS is that the CMS server itself can’t be included in the list of servers.


Reference:
 - [Free Course: SQL Server Management Studio Shortcuts & Secrets](https://sqlworkbooks.com/course/sql-server-management-studio-shortcuts-secrets/) (by Kendra Little)
 - [Fixing Hot-Key issue in SSMS in five steps](http://slavasql.blogspot.ru/2017/02/fixing-hot-key-issue-in-ssms-in-five.html) (by Slava Murygin)
 - [SSMS Tips and Tricks](http://www.ssmstipsandtricks.com/) (by Latish Sehgal)
 - [Do you need more than STATISTICS IO for Query Tuning?](https://www.sqlpassion.at/archive/2017/03/27/do-you-need-more-than-statistics-io-for-query-tuning/) (by  Klaus Aschenbrenner)
 - [](http://www.sqlmatters.com/Articles/Top%2010%20SQL%20Server%20Management%20Studio%20(SSMS)%20Tips%20and%20Tricks.aspx) (by )
 - [Keyboard shortcut to close a query tab in SSMS](https://www.am2.co/2017/01/close-ssms-tab/) (by Andy Mallon)
 - [SQL Server Management Studio Tips](https://www.mssqltips.com/sql-server-tip-category/52/sql-server-management-studio/)