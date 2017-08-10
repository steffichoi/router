# router

### OVERVIEW
We decided to structure our code so that all the nat functionality is in sr_nat.c.  Other than that, the application of the nat functionslity is implemented within one function in sr_router.c.

Additional functions other than what was provided in the starter code:
#### sr_nat.c
sr_nat_insert_mapping_unsol:
	inserts the unsolicited packet associated with the connection into the mapping
	this function is called in sr_nantHandle(), when processing packets received on the 
	external interface, and no mapping already exists for the intended destination

sr_nat_delete_mapping:
	delets the mapping
	this funciton is called in sr_nat_timeout(), to clean up the ICMP/TCP mappings that have become stale

sr_nat_ext_ip:
	set the external ip address to the ip of interface eth2	
	this funciton is called in sr_vns_comm.c when nat mode is enabled

sr_nat_delete_connection:
	closes the connection
	this function is called in sr_nat_timeout() to delelte a connection whenever an ICMP/TCP establish/TCP transitory timeout has occured
	it is also called in sr_nat_handle_external_conn() and sr_nat_handle_internal_conn() to close connections

sr_nat_handle_external_conn:
	handles all of the connections on the external interface and keeps track of the conneciton states

sr_nat_handle_internal_conn:
	handles all of the connections on the internal interface ane keeps track of the conection states

#### sr_router.c
sr_natHandle:
	determines if the packet was received on an internal or external interface and translates the packet accordingly
	in both cases, it looks for a mapping and if it does not exist, a new map is inserted using sr_nat_insert_mapping_unsol()
	if a map does exist then the packet is translated and forwarded
	this funciton is called in sr_handlepacket() when an ip packet is received and nat ode is enabled

tcp_cksum:
	like cksum, but for tcp


### DESIGN DECISIONS

We decided to handle the internal and external connections withtwo different functions to keep the code more organized, howeever in sr_natHandle, we decided that it would be more effecient to handle internal and external packets in one function so that when nat mode is enabled, only one function is called.
Other than that, the additional functions in sr_nat.c helps with the clarity and organization of the code.

We also decided to use a github repository for ease of transferring files and for multiple access, and to use Trello for issue tracking.  





