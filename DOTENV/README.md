## NodeJs DotEnv

#### installation section 
```javascript
//installation section 
npm i dotenv
```
#### Required section
```javascript
require('dotenv').config();
const data= process.env.DATABASE_UR
```
### Inside Dot Env File
```javascript
//Inside the .env File Eill Write In thise Wahy
DATABASE_URL=postgres://postgres:12345@localhost:5432/chate
PORT=3050
ACCESS_TOKEN_SECRET=lithhalim
REFRESH_TOKEN-SECRET=lithhalim
```

## React DotEnv
#### Installation section
```javascript
npm i react-dotenv
```
#### Required section
```javascript
import env from "react-dotenv";
const data=process.env.REACT_APP_DATA
```
#### Inside Dot Env File
```javascript
REACT_APP_DATA=SAHSHKJAHSJAHSKHAKJSHAJ//the propertuy must start REACT_APP
```