Download Link: https://assignmentchef.com/product/solved-cse3055-homework-7
<br>
Consider the <em>Turkish Super League</em> database accompanied with this homework.

<strong><em>Player</em></strong><em> (<u>PlayerID</u></em><em>: int</em><em>,   FirstName</em><em>: nvarchar(25)</em><em>,   LastName</em><em>: nvarchar(25)</em><em>,   Nationality</em><em>: varchar(25)</em><em>,   Birthdate</em><em>: smalldatetime</em><em>,   Age</em><em>: smallint</em><em>,   Position</em><em>: varchar(25)</em><em>) </em>

<strong><em>Team</em></strong><em> (<u>TeamID</u></em><em>: int</em><em>,   Name</em><em>: nvarchar(50)</em><em>,   City</em><em>: nvarchar(25)</em><em>) </em>

<strong><em>PlayerTeam</em></strong><em> (<u>PlayerID</u></em><em>: int</em><em>,   <u>TeamID</u></em><em>: int</em><em>,   <u>Season</u></em><em>: varchar(5)</em><em>) </em>

<h1><strong>Match</strong> (<u>MatchID</u>: int,   HomeTeamID: int,   VisitingTeamID: int,   DateOfMatch: smalldatetime,   Week: tinyint)</h1>

<strong><em>Goals</em></strong><em> (<u>MatchID</u></em><em>: int</em><em>,   <u>PlayerID</u></em><em>: int</em><em>,   IsOwnGoal</em><em>: bit</em><em>,   <u>Minute</u></em><em>: tinyint</em><em>) </em>




<u>Notes</u>:

<ul>

 <li>Table <em>Match</em> stores data only for season 2013-2014.</li>

 <li>Table <em>Goals</em> stores data only for season 2013-2014.</li>

</ul>

<strong>1)</strong> Table creation and data insertion.

<ol>

 <li><strong>a)</strong> [2 pts] Run the following queries to create the tables <em>Standings</em> and <em>TransactionLog</em> in your database. Create Table Standings (</li>

</ol>

Pos tinyint,

[Team Name] nvarchar(30),

GP tinyint,

W tinyint,

T tinyint,

L tinyint,

GF smallint,

GA smallint,

GD smallint,

Pts tinyint

)




Create Table TransactionLog ( LogID int identity(1,1) primary key,

LogTime datetime,

LogType char(1),

BeforeState nvarchar(500),

AfterState nvarchar(500),

)




<ol>

 <li><strong>b)</strong> [8 pts] In only one “insert into” statement; write a query to insert the output data of your stored procedure <em>sp_GetStandingsUpToDate(‘20140715’)</em> that you have in homework #6 into table <em>Standings</em>.</li>

</ol>

<strong>              </strong>

<strong>2)</strong>  Implement a trigger <em>Trg_RearrangeStandings</em> with the followings:

<ul>

 <li>When a record is inserted into, deleted from or updated on the table <em>Goals</em> (any change for <em>MatchID</em>, <em>PlayerID</em> and/or <em>IsOwnGoal</em>); then rearrange the table <em>Standings</em>, and insert a relevant record into the table <em>TransactionLog</em>.</li>

 <li>In all type of operations (insert, delete, update); <em>PlayerID</em> in table <em>Goals</em> must be a player of either the home team or the visiting team for that match in season 13-14. In any wrong match-team-player assignments, the transaction will be rolled back and any further executions will be stopped.</li>

 <li>A value less than 1 or greater than 90 cannot be entered in the field <em>Minute</em>.</li>

 <li><em>LogTime</em> is the time of operation.</li>

 <li><em>LogType</em> is “I” for insertion, “D” for deletion and “U” for update operation/transaction.</li>

 <li><em>BeforeState</em> is null for insertion and <em>TransactionLog.AfterState</em> is null for deletion. For update operation, <em>BeforeState</em> is the one before the operation and <em>AfterState</em> is the one after the operation.</li>

 <li>For the fields <em>BeforeState</em> and <em>AfterState</em> in table <em>TransactionLog</em>, concatenate all the related fields (<em>MatchID</em>, <em>PlayerID</em>, <em>IsOwnGoal</em>, <em>Minute</em>) in table <em>Goals</em> and separate them by a semicolon (e.g. ’306;324;0;58’) and enter this data in the fields <em>BeforeState</em> and <em>AfterState</em>, accordingly.</li>

</ul>