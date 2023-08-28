-- DAY2

--Exercise 1:
--Ans1 Query:
select distinct starttime from cd.bookings left join cd.members using(memid) where firstname='David' and surname='Farrell'

select avg(replacement_cost) from film group by (replacement_cost);


--Exercise 2:
--Ans1 Query:
select count(*)  from cd.facilities

--Ans2 Query:


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
select facs.name, sum(slots * case
                                  when memid = 0 then facs.guestcost
                                  else facs.membercost
    end) as revenue
from cd.bookings bks
         inner join cd.facilities facs
                    on bks.facid = facs.facid
group by facs.name
order by revenue;

