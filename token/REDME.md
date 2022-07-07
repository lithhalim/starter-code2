# 5-token
# accsess token 


## require 
```javascript
const jwt = require('jsonwebtoken');
require('dotenv').config();
```

## implimentation
```javascript
//create the acces token
module.exports= createAccessToken =(user)=> jwt.sign({
    //the information will save in peload section information of user
    @@@ input all data need  send in payload
    },
    //the secrete you use in the access token
    process.env.ACCESS_TOKEN_SECRET ,
    //the token will expire after these time
    {expiresIn:"7d"});

```

# refresh token
## require
```javascript
const jwt = require('jsonwebtoken');
require('dotenv').config();
```

```javascript
//create the refresh token 
module.exports= createRefreshToken =(user)=> jwt.sign({
    //the information will save in peload section information of user
    @@ all information you want sent in token
    },
    //the secrete you use in the access token
    process.env.ACCESS_TOKEN_SECRET ,
    //the token will expire after these time
    {expiresIn:"7d"});

```
