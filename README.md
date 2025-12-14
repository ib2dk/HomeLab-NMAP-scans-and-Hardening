# HomeLab-NMAP-scans-and-Hardening
Nmap scanning, vulnerability assessment, and hardening steps for home lab.


  Hosts Identified:  

  IP Address       System                    Purpose                                                                                            
  192.168.100.10  Windows Server            WinRM / Management testing  
  192.168.100.30   Windows 11                IIS Web Server              
  192.168.100.50   Linux                     Splunk Server               
  192.168.100.40   Unknown / Hardened Host   No exposed services
sudo nmap  sS   top ports 20 192.168.100.0/24
   
 bash
sudo nmap  sU   top ports 20 192.168.100.0/24
