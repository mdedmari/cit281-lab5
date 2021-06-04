![Image of allStudents](https://i.ibb.co/MSSzPzj/All-Students.png)
![Image of singleStudents](https://i.ibb.co/yhtMwRY/Single-Studnet.png)
![Image of unmatched](https://i.ibb.co/QHrGByW/Unmatched.png)

```
{
 const students = [
    {
      id: 1,
      last: "Last1",
      first: "First1",
    },
    {
      id: 2,
      last: "Last2",
      first: "First2",
    },
    {
      id: 3,
      last: "Last3",
      first: "First3",
    }
  ];

// Require the Fastify framework and instantiate it
const fastify = require("fastify")();
// Handle GET verb for / route using Fastify
// Note use of "chain" dot notation syntax

//Student Route
fastify.get("/cit/students", (request, reply) => {
    let studentIDFromClient = request.params.id;
    console.log(studentIDFromClient);

    let studentRequestedFromClientID = null;

    for (studentInArray of students) {
        if (studentInArray.id == studentIDFromClient){
            studentRequestedFromClientID = studentInArray;
            break;
        }
    }
    if (studentRequestedFromClientID != null) {
        reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(studentRequestedFromClientID);
    }
    else {
        reply
    .code(404)
    .header("Content-Type", "text/html; charset=utf-8")
    .send("<h1>No student with the given ID was found.</h1>");
    }
  
});

//Student ID Route
fastify.get("/cit/students/:id", (request, reply) => {
    reply
      .code(200)
      .header("Content-Type", "text/html; charset=utf-8")
      .send("<h1>At Student ID Route</h1>");
  });

  //Unmapped / Wild Card Route
fastify.get("*", (request, reply) => {
    reply
      .code(200)
      .header("Content-Type", "text/html; charset=utf-8")
      .send("<h1>At Unmatched Route</h1>");
  });

   // Add a student
fastify.post("/cit/students/add", (request, reply) => {
// 1) Get request from client
let userData = JSON.parse(request.body)
console.log(userData);
reply
      .code(200)
      .header("Content-Type", "text/html; charset=utf-8")
      .send("<h1>Added POST request</h1>");
 
});



  const listenIP = "localhost";
  const listenPort = 8080;
  fastify.listen(listenPort, listenIP, (err, address) => {
      if (err) {
          console.log(err);
          process.exit(1);
      }
     
    console.log(`Server listening on ${address}`);
  });

}
```
```
{
 {
  "name": "lab-05",
  "version": "1.0.0",
  "description": "",
  "main": " fastify-server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "fastify": "^3.15.1"
  }
}

}
```
