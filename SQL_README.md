--Ans1 query:
select * from cd.facilities

--Ans2 query:
select name, membercost from cd.facilities

--Ans3 query:
select * from cd.facilities where membercost > 0

--Ans4 query:
select facid,name,membercost,monthlymaintenance from cd.facilities where membercost >0 AND membercost < monthlymaintenance/50

--Ans5 query:
select * from cd.facilities where name Like '%Tennis%'

--Ans6 query:
select * from cd.facilities where facid in (1,5)

--Ans7 query:
select name, case when monthlymaintenance >100 then 'expensive' else 'cheap'
end as cost from cd.facilities

--Ans8 query;
select memid, surname, firstname, joindate from cd.members where joindate >= '2012-09-01 00:00:00'

--Ans9 query:
select distinct surname from cd.members order by surname limit 10

--Ans10 query:
select distinct surname from cd.members
union
select distinct cd.facilities.name from cd.facilities

--Ans11 query:
select joindate as latest from cd.members order by joindate desc limit 1

--Ans12 query:
select firstname,surname,joindate from cd.members order by joindate desc limit 1 