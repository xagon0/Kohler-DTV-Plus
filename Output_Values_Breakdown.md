## Functions and requests that return values 
The requests below are for returning information from the controller. 
They can cause errors, lockups, and general problems up to and including removal of the software running on the controller. *Proceed with caution.*

Due to the way the controller returns results (inside of a buffered socket), headers are often invalid and most requests fail in tools like Postman, SoapUI, and PowerShell.
In-browser requests will normally function with Chrome.

Landing URL -> cgi_landing_url
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
