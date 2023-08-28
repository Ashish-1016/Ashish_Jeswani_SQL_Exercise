-- DAY2

--Exercise 1:
--Ans1 Query:
select distinct starttime from cd.bookings left join cd.members using(memid) where firstname='David' and surname='Farrell'

--Ans2:
select avg(replacement_cost) from film group by (replacement_cost);

--Ans3:
select distinct recs.firstname as firstname, recs.surname as surname
from cd.members mems
inner join cd.members recs
on recs.memid = mems.recommendedby
order by surname, firstname;

--Ans4:
select mems.firstname as memfname, mems.surname as memsname, recs.firstname as recfname, recs.surname as recsname
from cd.members mems
left outer join cd.members recs
on recs.memid = mems.recommendedby
order by memsname, memfname;

--Ans5:
select distinct firstname || ' ' || surname as member, name as facility from cd.members inner join cd.bookings using(memid)
inner join cd.facilities using(facid) where cd.facilities.name in ('Tennis Court 1', 'Tennis Court 2') 
order by member, facility

--Ans6:
select mems.firstname || ' ' || mems.surname as member, facs.name as facility, 
case 
	when mems.memid = 0 then
		bks.slots*facs.guestcost
	else
		bks.slots*facs.membercost
	end as cost
from cd.members mems
inner join cd.bookings bks on mems.memid = bks.memid
inner join cd.facilities facs on bks.facid = facs.facid
where bks.starttime >= '2012-09-14' and  bks.starttime < '2012-09-15' and (
			(mems.memid = 0 and bks.slots*facs.guestcost > 30) or
			(mems.memid != 0 and bks.slots*facs.membercost > 30)
		)
order by cost desc;

--Ans7:
select distinct mems.firstname || ' ' ||  mems.surname as member, 
(select recs.firstname || ' ' || recs.surname as recommender from cd.members recs where recs.memid = mems.recommendedby)
from cd.members mems
order by member;


--Exercise 2:
--Ans1 Query:
select count(*)  from cd.facilities

--Ans2 Query:
select count(*) facid from cd.facilities where guestcost >=10

--Ans4 Query:
select facid, sum(slots)  from cd.bookings group by facid order by facid;

--Ans5 Query:
select facid, sum(slots) as "Total Slots"  from cd.bookings where starttime >= '2012-09-01' and starttime <= '2012-10-01' group by facid order by sum(slots);

--Ans6 Query:
select facid, extract(month from starttime) as month, sum(slots) as "Total Slots" from cd.bookings where extract(year from starttime)='2012'  group by facid, month order by facid, month;

--Ans7 Query:
select count(distinct memid) bookings from cd.bookings

--Ans8 Query:
select facid, sum(slots) as "Total Slots" from cd.bookings group by facid having sum(slots) >= 1000 order by facid;

--Ans9 Query:
select facs.name, 
sum(slots * case when memid = 0 then facs.guestcost
else facs.membercost
end) as revenue from cd.bookings bks
	inner join cd.facilities facs
	on bks.facid = facs.facid
group by facs.name
order by revenue;

