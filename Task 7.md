**TASK 7: Abusing Vulnerable software**

In this task we have the machine which have **Druva inSync 6.6.3** on it and according to some previous research they have found out that the port 6064 with system priv is always open we have the exploit in the 
task itself we just have to change **Two parameters** in it and after doing so we will be able to spawn a session under the user `pwnd`.


You can find the vuln file in `C:\tools`

Edit that vuln and add your user to it using the command :

    "net user pwnt pAsS321 /add & net localgroup administrators pwnt /add"

After this save the script and then open the `Window Powershell ISE` and run the scrip over there and check wether the user has been added or not using the comamnd

    net user pwnt
![Screenshot 2023-10-25 140439](https://github.com/Theincognitomode/Windows-Privilege-Escalation-WriteUP/assets/73027020/ae88ddbe-c2c3-4e1c-989f-40b70f0baf87)

As we can see the user has been added as well as pressent in the administrators group

Now open the cmd as administrator then click on more choices and choose your user that you have added enter the pass and then you can get the flag 


![Screenshot 2023-10-25 140721](https://github.com/Theincognitomode/Windows-Privilege-Escalation-WriteUP/assets/73027020/cb92c4a4-216d-4150-938d-dd3ff7625e73)

And now you will get a prompt type the command as :
    
    type C:\Users\Administrator\Desktop\flag

![Screenshot 2023-10-25 141058](https://github.com/Theincognitomode/Windows-Privilege-Escalation-WriteUP/assets/73027020/610cee2e-20ca-4980-9c54-40b718552b83)

And there we have the flaggg...

    THM{EZ_DLL_PROXY_4ME}
