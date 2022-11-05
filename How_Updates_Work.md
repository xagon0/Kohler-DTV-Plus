## How updates for the DTV+ controller and modules work 
This section covers a general overview on how the DTV+ controller aquires updates, and processes them.
Please note that the following is a generalized *opinion* based on traffic captures, decompilation, and other ascertained information.

Overview
------ 
A brief overview of the update process looks like the following:
+ The controller is told to check for updates. This can be:
  + Calling  `http://controller_ip/check_updates.cgi` which sets a 'check for updates' variable to true. `BYTE_G[34]`
  + Through a computed value which determines a time to check each day.
    + The calculation below determines what time of day to process the update.
     ```cpp  
         //Adjusted for clarity
         
         if(((minutes_after_midnight / 10) == (First4SerialNumber % 144)) 
         && ((minutes_after_midnight % 10) == 0))
         {
            Check_For_Update = 1;
         }
         
         //Check_For_Update = BYTE_G[34] 
         //First4SerialNumber = WORD_S[32]
     ```
    + If you wish to determine your update time, the simple calculation is: `(First4SerialNumber % 144) * 10 = Update_Time_In_Minutes_After_Midnight`
+ Verify no images are being written / downloaded. 
+ Verify internet access by resolving `*redacted*.kohler.com`, then pinging the IP address.
+ If access is confirmed, connect to a public ftp located at `*redacted ip address*` using the username: `ftpuser`, and password `*redacted*`
+ Attempt to access folder "00", but if the `const_hospitality` string `STRING_S[39]` has been set, attempt to download from that folder.
+ Download and parse the `versions.txt` file, store latest version of controller in `STRING_S[27]` and latest version of ui_amulet in `STRING_S[29]`
+ Confirm if the values are newer than the existing.
+ Download new if required.
+ Trigger processor event to process image swap.
