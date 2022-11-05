## How updates for the DTV+ controller and modules work 
This section covers a general overview on how the DTV+ controller aquires updates, and processes them.
Please note that the following is a generalized overview based on traffic captures, decompilation, and other verifiable information.

Overview
------ 


###### Details
* Address: `http://controller_ip/landing_url.cgi`
* Description: Returns the url for the landing page (ie: the url to redirect to after entering the controller ip address).
* Additional Details: Early versions of the controller software may have redirected between the control.html page and settings.html page depending on device count. I have not been able to confirm this, and basic decompliation appears that this request always result in a hardcoded `{"url":"settings.html"}` result.

###### Call Safety Rating
✅ - 0/5 - Appears to be safe to call.

###### Params
No params supported for this function

###### Example Request
`http://controller_ip/landing_url.cgi`

###### Example Result
```json
{"url":"settings.html"}
```
