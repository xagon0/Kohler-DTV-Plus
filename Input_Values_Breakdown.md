## Functions and requests that save values 
The requests below are for updating and adjusting values inside the controller. 
They can cause errors, lockups, and general problems up to and including removal of the software running on the controller. *Proceed with caution.*

Due to the way the controller returns results (inside of a buffered socket), headers are often invalid and most requests fail in tools like Postman, SoapUI, and PowerShell.
In-browser requests will normally function with Chrome.

Mac -> cgi_mac
------ 
###### Details
* Address: `http://controller_ip/mac.cgi`
* Description: Sets a new mac address for the controller.

###### Call Safety Rating
⚠️ - 3/5 - Appears to function, but often results in controller locking up. 
Not to mention, you really shouldn't change this value.

###### Params
| Key | Value | Description |
| --- | --- | --- |
|first|00 to FF|first octet of new mac|
|second|00 to FF|second octet of new mac|
|third|00 to FF|third octet of new mac|
|fourth|00 to FF|fourth octet of new mac|
|fifth|00 to FF|fifth octet of new mac|
|sixth|00 to FF|sixth octet of new mac|

###### Example Request
`http://controller_ip/mac.cgi?first=00&second=1A&third=2B&fourth=3C&fifth=4D&sixth=5F`

###### Additional Details
```cpp
    //Directly written to the NAND

    //Subtask appears to move this into the DataTable:
    WORD[16]     //First Four Digits as Decimal
    WORD[17]     //Middle Four Digits as Decimal
    WORD[18]     //Last Four Digits as Decimal
    
```

Serial -> cgi_serial
------ 
###### Details
* Address: `http://controller_ip/serial.cgi`
* Description: Sets a new serial number for the controller.

###### Call Safety Rating
⚠️ - 3/5 - Appears to function, but often results in controller locking up. 
Not to mention, you really shouldn't change this value.

###### Params
| Key | Value | Description |
| --- | --- | --- |
|first|00 to FF|first octet of new serial|
|second|00 to FF|second octet of new serial|
|third|00 to FF|third octet of new serial|
|fourth|00 to FF|fourth octet of new serial|

###### Example Request
`http://controller_ip/serial.cgi?first=00&second=1A&third=2B&fourth=3C`

###### Additional Details
```cpp  
    //Stored in DataTable:
    WORD[32]     //First Four Digits as Decimal
    WORD[33]     //Last Four Digits as Decimal
```
