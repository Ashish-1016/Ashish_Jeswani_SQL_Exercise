--Day3
--Table Operations
--Ans1:
insert into cd.facilities (facid,name,membercost,guestcost,initialoutlay,monthlymaintenance)
values (9,'Spa',20,30,100000,800)

--Ans2:
insert into cd.facilities (facid,name,membercost,guestcost,initialoutlay,monthlymaintenance)
values (9, 'Spa',20,30,100000,800),(10, 'Squash Court 2', 3.5,17.5, 5000,80)

--Ans3:
insert into cd.facilities
(facid,name,membercost,guestcost,initialoutlay,monthlymaintenance)
values ((select max(facid) from cd.facilities)+1, 'Spa',20,30,100000,800)

--Ans4:
update cd.facilities set initialoutlay = 10000 where name in ('Tennis Court 2')

--Ans5:
update cd.facilities set membercost=6, guestcost=30 where facid in (0,1)

--Ans6:
update cd.facilities facs
set
    membercost = (select membercost * 1.1 from cd.facilities where facid = 0),
    guestcost = (select guestcost * 1.1 from cd.facilities where facid = 0)
where facs.facid = 1;

--Ans7:
delete from cd.bookings

--Ans8:
delete from cd.members where memid=37

--Ans9:
delete from cd.members where memid not in (select memid from cd.bookings)


--Day 3
--String Function

--Ans1:
select surname || ', ' || firstname as name from cd.members

--Ans2:
select * from cd.facilities where name like 'Tennis%'

--Ans3:
select * from cd.facilities where lower(name) like 'tennis%'

--Ans4:
select memid, telephone from cd.members where telephone similar to '%[()]%' order by memid

--Ans5:
select lpad(cast(zipcode as char(5)),5,'0') zip from cd.members order by zip

--Ans6:
select substring(surname,1,1) letter, count(substring(surname,1,1)) from cd.members group by letter order by letter

--Ans7:
select memid,translate(telephone, '-() ','') telephone  from cd.members order by memid
