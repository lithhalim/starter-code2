## 🔗 SOKET IO SERVER


## 🔗 Normal Connection 
```javascript
io.on("connection", (socket) => {
  // you will emit the data just for sender
  socket.emit(/* ... */);

  // to all clients in the current namespace except the sender
  socket.broadcast.emit(/* ... */);

  //get data from the sender clinet
  socket.on(/* ... */)


  // to all clients in namespace "myNamespace"
  io.of("myNamespace").emit(/* ... */);

  // to all clients in room1 in namespace "myNamespace"
  io.of("myNamespace").to("room1").emit(/* ... */);
});


```


## 🔗 Room Server Side

```javascript
//clinet will send data to join specific room *join room*
soket.on("JoinToRoom",(data)=>{
        soket.join(data)
    })

// to all clients in room1 except the sender
  socket.to("room1").emit(/* ... */);

// to all clients in room1
  io.in("room1").emit(/* ... */);


```
## 🔗 NameSpace

```javascript
const adminNamespace = io.of("/admin");

//name space like root
  // to all clients in namespace "myNamespace"
  adminNamespace.emit(/* ... */);

  // to all clients in room1 in namespace "myNamespace"
  adminNamespace.to("room1").emit(/* ... */);


```
## 🔗 Disconnect
```javascript
  soket.on("disconnect", () => {
    console.log("desconnect")

  })
```





## 🔗 CLINET SIDE

```javascript
// basic emit
socket.emit(/* ... */);

// with acknowledgement
socket.emit("question", (answer) => {
  // ...
});

```


## 🔗 Soket Io Connection with express js
```javascript
$npm install socket.io

```
## 🔗 implimentation

```javascript

const app = require("express")();
const httpServer = require("http").createServer(app);
const options = { /* ... */ };
const io = require("socket.io")(httpServer, options);

io.on("connection", socket => { /* ... */ });

httpServer.listen(3000);
// WARNING !!! app.listen(3000); will not work here, as it creates a new HTTP server

```
