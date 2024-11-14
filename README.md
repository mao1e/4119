Jonathan Ang
ma4624
Project 1 Final Stage

proxy:	this is a proxy that acts as a server to which clients can connect to to obtain html and video files.
	it then acts as a client, requestng a server ip from the dns server listed in the topology, then
	requesting the html and video files from the server ip using tcp. The proxy measures the throughput
	and asks for video chunks using the most suitable bitrate corresponding to the throughput. It logs these
	throughput measurements in a seperate file
	usage:
	./proxy <topo-dir> <log> <alpha> <listen-port> <fake-ip> <dns-server-port>

	log: The file path to which you should log the messages described in Logging.

	alpha: A float in the range [0, 1]. Use this as the coefficient in your EWMA throughput estimate.

	listen-port: The TCP port your proxy should listen to for accepting connections from your browser. 

	fake-ip: Your proxy should bind to this IP address for outbound connections to the web servers. The fake-ip can only be one of the clients’ IP addresses under the network topology you specified (see Network Simulation). The main reason why we are doing this is because netsim emulates a network topology where it can manipulate throughput on links between end-hosts. If we bind the outbound socket to this fake-ip, then we can be sure that packets sent between the proxy and the server traverse ONLY the links set by netsim. (and here is why you want your packets to traverse netsim links only)

	dns-server-port: The port on which you run your DNS server (see Running the DNS Server)


dns_server:	this received a dns request and then uses either round robin or lowest latency to provide a server_ip
		lowest latency is measured and logges by sending a ping to each server ip
		round robin alternates between the servers.
		usage: ./dns_server <topo-dir> <log> <listen-port> <decision-method>
		topo-dir: Directory corresponding to the topology you’re using in the experiment. Here your DNS server will find the IP address it should listen on, and the video server addresses.

		log: The file path to which you should log the messages described in Logging.

		listen-port: The UDP port your proxy should listen on for accepting DNS requests. 

		decision-method: One of “round-robin” or “lowest-latency”. See Choosing the Best Web Server for more information.

