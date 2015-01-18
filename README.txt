Project 4: PortScanner
-----------------------

Name: Vivek Supe		
uname: vsupe

Name: Jay Modi	
uname: jmmodi

------------------------

This is a partial emulation of port analysis tool like nmap ("Network Mapper") which send customized packets and analyze packets being received over a LAN/Link. One prominent use of this information is in troubleshooting network configuration, security and reachability. We have used SOCK_RAW to create customized UDP packets with checksums with a special case of an DNS packet which queries DNS server with a question, TCP SYN NULL XMAS FIN ACK with checksums and finally we checked services of few well known ports like 80,22,43,143,110,etc.

Files Includes With This Project:
	PortScanner.cpp 	pssetup.cpp		pssetup.h 		TCPUDPScan.cpp		TCPUDPScan.h 		makefile

Tasks Accomplished:
	+ Created RAW Sockets
	+ Used Poll() to poll between two SocketFileDescriptors
	+ Created TCP/UDP Packets
	+ Created specialized packets like DNS with question query
	+ Check For All Services from 1-1024 Ports
	+ Check well known services versions. (SSH,IMAP,SMTP,WHOIS,POP,HTTP)

Guide:

1 - Type WIN:"echo %cd%: or for LINUX:"pwd" so check current directory. Now we use "cd" to change directory to the folder which has the Makefile & C File.
2 - We compile the file. To do so we have to get into current directory where the code is based and type "$make" command.
3 - Once the code has compiled we can go ahead with running the program. So do so we first understand the flags used.
        	 .“./portScanner [option1, ..., optionN]”. 
        	 Some valid options:
			• --help. Example: “./portScanner --help”.
			• --ports <ports to scan>. Example: “./portScanner --ports 1,2,3-5”.
			• --ip <IP address to scan>. Example: “./portScanner --ip 127.0.0.1”.
			• --prefix <IP prefix to scan>. Example: “./portScanner --prefix 127.143.151.123/24”.
			• --file <file name containing IP addresses to scan>. Example: “./portScanner --file filename.txt”.
			• --speedup <parallel threads to use>. Example: “./portScanner --speedup 10”.
			• --scan <one or more scans>. Example: “./portScanner --scan SYN NULL FIN XMAS”.

Understanding Outputs:
	1- sudo ./portScanner --ports 22,53,80-90 --scan ACK --ip dagwood.soic.indiana.edu --speedup 5
		IP address :	129.79.247.87
		Port	Service Name	Service Version		Result						Conclusion
		----------------------------------------------------------------------------------------------------------------------------
		22	ssh			-			(ACK)UNFILTERED		Filtered
		82	UnAssigned		-			(ACK)UNFILTERED		Filtered
		81	UnAssigned		-			(ACK)UNFILTERED		Filtered
		53	domain			-			(ACK)UNFILTERED		Filtered
		80	http		HTTP Server: Apache/2.2.15 	(ACK)UNFILTERED		Filtered
		83	UnAssigned		-			(ACK)UNFILTERED		Filtered
		85	UnAssigned		-			(ACK)UNFILTERED		Filtered
		84	UnAssigned		-			(ACK)UNFILTERED		Filtered
		87	link			-			(ACK)UNFILTERED		Filtered
		86	UnAssigned		-			(ACK)UNFILTERED		Filtered
		90	UnAssigned		-			(ACK)UNFILTERED		Filtered
		88	kerberos		-			(ACK)UNFILTERED		Filtered
		89	UnAssigned		-			(ACK)UNFILTERED		Filtered

		Total Time Taken: 0.235141
	2- sudo ./portScanner --ports 80-90 --scan SYB --ip dagwood.soic.indiana.edu --speedup 2
	IP address :	129.79.247.87
	Port	Service Name	Service Version		Result						Conclusion
	----------------------------------------------------------------------------------------------------------------------------
	80	http		HTTP Server: Apache/2.2.15 	(SYN)OPEN		Open
	22	ssh			-			(SYN)OPEN		Open
	81	UnAssigned		-			(SYN)CLOSED		Closed
	82	UnAssigned		-			(SYN)CLOSED		Closed
	83	UnAssigned		-			(SYN)CLOSED		Closed
	85	UnAssigned		-			(SYN)CLOSED		Closed
	84	UnAssigned		-			(SYN)CLOSED		Closed
	87	link			-			(SYN)CLOSED		Closed
	86	UnAssigned		-			(SYN)CLOSED		Closed
	88	kerberos		-			(SYN)CLOSED		Closed
	89	UnAssigned		-			(SYN)CLOSED		Closed
	90	UnAssigned		-			(SYN)CLOSED		Closed
	Total Time Taken: 0.268804

