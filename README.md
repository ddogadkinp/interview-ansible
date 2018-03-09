# Interview Question Overview

In this interview question we would like to build an ansible playbook
that will install NGINX and multiple nodeJS based HTTP servers on local CentOS/RHEL machine. The playbook should expect to recieve number of NodeJS HTTP server to install as input variable. You would be given a simple 12 line NodeJS HTTP server code, which will have a setting for a port and a default message. You goal is to develop the playbook to dynamically create nodeJS based HTTP servers running behind NGINX proxy.

## Development Environment

For this test we will be using AWS Cloud9. This environment is an online IDE and has console which has ansible installed. This allows you to run ansible commands.

## Interview Question Requirements

Write ansible playbook that will:
1. Install NGINX on local CentOS/RHEL machine 
2. Install NodeJS on local CentOS/RHEL server if not installed 
3. Dynamically configure NGINX to provide proxy paths for every nodeJS HTTP server that will be created 
4. Dynamically create all the NodeJS HTTP servers 
5. Use pm2 as a process controller for NodeJS HTTP servers 
6. Start NGINX and NodeJS HTTP servers at appropriate times

## NodeJS HTTP servers code

This is the code for the NodeJS HTTP server to be placed in index.js:
```
const http = require('http')
const port = 3000
const requestHandler = (request, response) => {
  console.log(request.url)
  response.end('Hello Node.js ServerX!') }
const server = http.createServer(requestHandler)
server.listen(port, (err) => {
  if (err) {
    return console.log('something bad happened', err)  }
  console.log(`server is listening on ${port}`)
})
```
### How to RUN NodeJS HTTP server with pm2

`pm2 start <location_of_index_js>/index.js`
    - to start a single NodeJS HTTP server 
`sudo pm2 startup` 
    - to setup init scripts
`pm reload <ecosystem_config_file> --update-env` 
    - to reload nodejs apps ecosystem