### Iterated VS Recursive DNS queries
- Iterated
	- Exhaustively Iterates through all the DNS servers horizontally and then goes down a level
- Recursive
	- Server that is queried then takes the responsibility to get a response for the query back to the sender
### Aliasing & Load Balancing

### DNS Caching

### DNS Security
- DOS/DDOS
- Hijacking DNS
	- Threat Model and Attacker Goals 
	- Doesnt work now due to Bailiwick Checking, contextual updates only
- Kaminisky Exploit
	- PreReq is that local nameserver must not have the original website cached