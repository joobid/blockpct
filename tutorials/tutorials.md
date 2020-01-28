# Trust OS Tutorials


In this section you will find snipets of code to integrate API calls to your page



## NodeJS


### Axios library

Axios is a promise based HTTP client for the browser. Using promises is great when dealing with code that requres chains of events.



```javascript
const axios = require('axios');

axios.post('https://trustapi.tid.es/trust/asset', {
 headers: {
   Authorization: 'Bearer ' + token // Token is a variable that stores the JWT
},
  body: {
    'input':'whatever'
  })
  
  .then(response => {
    console.log(response.data.url);
    console.log(response.data.explanation);
  })
  .catch(error => {
    console.log(error);
  });
```


### HTTP

If you dont want to use third party libraries,you can use node http standard module. However, this option is a little more verbose than the preceding one

```javascript

const https = require('https')

const data = JSON.stringify({
  input: 'whatever'
})

const options = {
  hostname: 'https://trustapi.tid.es/',

  path: '/trust/asset/create',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Content-Length': data.length,
    'Authorization': 'Bearer '+token  // Where token is the JWT 
  }
}

const req = https.request(options, (res) => {
  console.log(`statusCode: ${res.statusCode}`)

  res.on('data', (d) => {
    process.stdout.write(d)
  })
})

req.on('error', (error) => {
  console.error(error)
})

req.write(data)
req.end()

```




## PYTHON

### Requests

You dont really want to use any other module!

``` python
import requests

auth_token='kbkcmbkcmbkcbc9ic9vixc9vixc9v'
hed = {'Authorization': 'Bearer ' + auth_token}
data = {'app' : 'aaaaa'}

url = 'https://trustapi.tid.es/trust/asset'
response = requests.post(url, json=data, headers=hed)
print(response)
print(response.json())
```



## Shell

Lets not forget our old friend curl. This way can also be integrated in any other programming language calling something like exec.shell(command)


```shell
curl -X POST "https://trustapi.tid.es/trust/asset/create" -H "accept: application/json" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MTEyMjMwOX0.Qu28A580dTOXPAX9bKsnEuHRk8NxFLGL0iPkK5RuOKg" -H "Content-Type: application/json" -d "{ \"assetid\": \"1\", \"data\": {}, \"metadata\": {}, \"registerInEthereum\": \"true/false\"}"
```



