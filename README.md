# System-design-cheat-sheet
work to record my progress in the arena of system design



## Workflow
source: https://www.youtube.com/watch?v=-W9F__D3oY4
<br/>
### vertical and horizontal scaling

CLIENT -----(sends request)----- DNS Server (host name to IP address)
<br/>
for horizontal scaling, we need a load balancer- that is a fancy DNS Server which follows a certain algorithm like *Round Robin* to distribute load among the servers or we can have dedicated servers where say, one server dedicated to all html requests and another server handles multimedia like images, gifs, etc

<br/>
**Caching** and **Time-to-live**
