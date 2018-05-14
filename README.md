# Attack-Reflector
Project of Software Security. 

Implemented RFC 2616 standard. 
When other host attacks victim(server), it sends back the packet to attacker, which was intended to target the victim. So essentially attacker 
attacks himself.

Implementated of ARP, IP  TCP, UDP protocols in scapy python library. Server listens and sends valid HTTP responses as well.


About the Program: 
This program is  a single executable, called reflector.

Interface
Command line interface:

./reflector --interface eth0 --victim-ip 192.168.1.10  --victim-ethernet 31:16:A9:63:FF:83 --reflector-ip 192.168.1.20 --reflector-ethernet 38:45:E3:89:B5:56

Listens to the given network interface, and any IP, TCP, or UDP packets sent to the given victim IP address should be taken and sent (without modification) on the given interface to the src IP from the reflector IP address. Then, when there is a response from the src IP address to the reflector IP address, that response should be sent back to the src IP address as if it was from the victim IP address.

In this way, program will impersonate two IP address (victim and reflector), and any packets that are sent to the victim will get resent to the src IP from the reflector IP. One good way to test this is to try to SSH to the victim IP from a machine that you have SSH access. You should find yourself SSHing into that same machine.


Testing
 script test_reflector.sh was provided which will allow you to test the reflector on a single Ubuntu 16.04 machine (without using a virtual machine or another computer on the network to simulate the attacker). This uses network namespaces, a Linux kernel feature that allows having multiple network namespaces. The script uses this feature to simulate having multiple computers on a network (by using a virtual ethernet device). 

First, download the test_reflector.sh script to the same directory that your reflector is in.

Then, make test_reflector.sh executable:

chmod +x ./test_reflector.sh
Then, run test_reflector (which will compile your reflector, set up the networking, run the reflector, then cleanup the networking)

./test_reflector
If everything goes correctly, you should see some instructions (which will document different ways to debug/test this environment), and from another terminal you can run ping 10.0.0.3 to try to ping the victim IP.
