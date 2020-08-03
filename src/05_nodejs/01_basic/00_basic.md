### Global ###
global variables  
https://nodejs.org/api/globals.html 

### First program 
Create js file 
hello.js
```javascript
const hello = "Hello node";
 
console.log(hello);
```

Run code
```bash
$ node hello
```

### required ### 
global.js
```javascript
required("path");

console.log(`The file name is ${path.basename(__filename)}`);
```

### process ###
Getting information about processes 
global.js
```javascript
console.log(process.id) //process id
console.log(process.versio.node) //node version
console.log(process.argv) //array containing process arguments
```