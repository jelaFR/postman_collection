 # Cisco DCNM (collection)
 - **Login to DCNM**
   - Login to DCNM and collect token (save it to **dcnm_token** var)
 - **Create tasks**
   - VRFs
     - Create
     - Attach
     - Deploy
   - Networks
     - Create
     - Attach
     - Deploy
   
 > Some fields on the creation tasks are left with default values
 > This requires a change from your side if you need to change these values
 
 > This collection will be greatly improved setting pre-login script
 > I've not finished this task, I miss the conversion of login:password to Base64 part in the following script
 ```javascript
 // Get Token from DCNM Login
pm.sendRequest({
    url: `https://${pm.environment.get("dcnm_url")}/rest/logon`,
    method: 'POST',
    header: {
        'content-type': 'application/json',
        'Host': `${pm.environment.get("dcnm_url")}`,
        'Authorization': 'Basic YWRtaW46QzFzY28xMjM0NQ==',
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    },
    body: {
        mode: 'raw',
        raw: JSON.stringify({expirationTime: 600000})},
    },
    function (err,res) {
        if (err) {
            console.log("Error during token collection");
        } else {
            console.log(`Result is: ${JSON.parse(res)}`);
            var jsonData = JSON.parse(res);
            postman.setEnvironmentVariable("dcnm_token", jsonData["Dcnm-Token"]);
            console.log("Error during token collection");
        }
    }
)
 ```
