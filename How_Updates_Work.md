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
+ if dim
+ then



* Address: `http://controller_ip/check_updates.cgi`
* Description: Sets a flag to check for an update on the next processor cycle. Always returns `{}`
* Additional Details: The update task appears to be part of a greater scope that hits other specific flags, possibly related to custom firmware for hotels. It's also noted that the generic internet check may have originally been `facebook.com` but was changed to `*redacted*.kohler.com`.

###### Call Safety Rating
✅ - 0/5 - Appears to be safe to call.

###### Params
No params supported for this function

###### Example Request
`http://controller_ip/check_updates.cgi`

###### Example Result
```json
{}
```
