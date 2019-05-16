# System-design-cheat-sheet
work to record my progress in the arena of system design



## Workflow
source: https://www.youtube.com/watch?v=-W9F__D3oY4
<br/>
### vertical and horizontal scaling

CLIENT -----(sends request)----- DNS Server (host name to IP address)
<br/>
https://stackoverflow.com/questions/11707879/difference-between-scaling-horizontally-and-vertically-for-databases
<br/>
for horizontal scaling, we need a load balancer- that is a fancy DNS Server which follows a certain algorithm like *Round Robin* to distribute load among the servers or we can have dedicated servers where say, one server dedicated to all html requests and another server handles multimedia like images, gifs, etc

<br/>

**Caching** and **Time-to-live**
<br/>

**Log-in sessions**- storing session data in external hard drives, like a database or a file server, for users so that the servers can share states. 
<br/>

*drawback*- what if the file server fails?
<br/>

*solution* - **RAID**
<br/>

## RAID - Redundant Array of Independent Disks
<br/>
approaches - striping and redundnacy
<br/>

*(**preferably throwing redundnacy to the confines of a single server**)*
<br/>
(necessary concerns - *scalabilty*, *versatility*, *economic*, *response time* )
<br/>

## Sticky sessions
<br/>
On multiple visits to a website, the session somehow gets preserved.
<br/>
MySQL does caching for identically executed queries (which happens when a user is navigating in a website)

## CAP
<br/>
CAP theorem states that : while desigining a distributed system, it is impossible to achieve all 3 objectives namely, consistency, availability and tolerance, simultaneously.
<br/>
1. consistency - updated information is available almost as soon as it is updated
<br/>
2. availability - always available for the clients
<br/>
3. partition tolerance - working doesn't stop in case of a communication loss
<br/>
http://ksat.me/a-plain-english-introduction-to-cap-theorem/
<br/>
some good reads
<br/>
https://www.quora.com/What-are-Master-and-Slave-databases-and-how-does-pairing-them-make-web-apps-faster
<br/>
https://medium.com/@Pinterest_Engineering/sharding-pinterest-how-we-scaled-our-mysql%20-fleet-3f341e96ca6f
<br/>
https://en.wikipedia.org/wiki/Paxos_(computer_science) 
<br/>



## Sharding 

<br/>
Sharding is a method of splitting and storing a single logical dataset in multiple databases. By distributing the data among multiple machines, a cluster of database systems can store larger dataset and handle additional requests. Sharding is necessary if a dataset is too large to be stored in a single database.
<br/>


## memcache

(memory cache)-powerful technique-used by fb for years- stores in RAM-implemented in many languages-used since responses from cache requests are faster than that from database queries
<br/>
facebook is more read heavy(than write heavy) as more than 10-20 updates can show on our newsfeed in a minute (which are actually some sort of queries), coz it is unlikely for us to update our own status (write into it) around 10-20 times in the same time (a minute).  
Hence, facebook prefers using memcache (that involves just a look up in the cache or memory), rather than executing heavy database queries. (facebook is dealing with billions of users, scanning the entire database is very costly).
<br/>


## Replication - the concept of master-slave

automatic copies of data in the master is generated in the slaves.
adavntages- ensures backup (master dies- promote a slave to a master-make necessary reconfigurations-it works!), can be used for load balancing, especially for read heavy websites like facebook, select queries can go to slaves for writing, whereas insert, upadte and delete deal with the master (we can have more servers to lighten the load further).

All in all, we have spare and read requests are balanced.
*we can have master-master paradigm too, in which we have 2 masters and write in either of them, and the code gets replicated in the other.*
<br/>


