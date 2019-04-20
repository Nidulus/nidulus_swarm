# nidulus_swarm
Nidulus MESH Swarm Controller

## Connecting the world

This neat little application will put all your machines/devices which share the same network in a shared MESH Swarm.\
Sending data to all other nodes on the network is as easy as doing a HTTP POST to http://localhost:your_configured_port/communicate

Originally created for quick syncing of data between devices.

#### Home page

https://swarm.nidulus.io

Feel free to also check out https://platform.nidulus.io were some of the code were borrowed from

### Prerequisites
Linux x64

### Description of nidulus_swarm

When you download and unzip the package you will find three ( 3 ) important files.

nidulus_swarm:        The application\
config/settings.json: The configuration\
svc.js:               The file containing onMessage function which is executed each time another node sent a message

### Getting started

1: Place the package on all machines/devices you want to swarm\
2: Unpack (duh)\
3: Edit the config/settings.json file (see below)\
4: Start the nidulus_swarm\
5: Use it (see below)

### Configuring

#### threads

Decide how many threads you want the app to run in. Higher value = higher throughput. Each receiver will still get 1x copy of each message, don't worry. No multiplying messages, just more juice.

It is useless to set a higher threads count than you actually have physical cpu cores (no, virtual doesn't count). This will slow the throughput rather than increase it.

Note that nidulus_swarm is written in NodeJS, meaning it does a lot of async even on one core and is fast. You might not need to increase this for your use-case.

#### security_key

Pick a 16 character long key. This is used for part of the encryption process (not exclusively though). With the default text in the settings.js you will not be able to run (it is too long). So change this.

Each node on your network that you want to swarm together, needs to use the same key. Otherwise the decryption fails and onMessage is never called.

#### rest.port

Set the port you want to use for the built-in webserver that handles your message sending to the swarm.

#### premium_license

If you have one of these, you will get three ( 3 ) additional endpoints available on the http server:

/counters   - HTTP GET - Lists 7 days history of messages counted sent/received. Each entry represents one hour.\
/network    - HTTP GET - Lists 7 days history of visible nodes in swarm. Each entry represents one minut.\
/statistics - HTTP GET - Lists 7 days history of hardware usage. Each entry represents 2 minutes.

Shown statistics for last endpoint includes: Process own memory usage, machine overall cpu usage, machine overall memory usage ( total + free), disk usage ( total + free ). More will be added.

### Running/Using

#### Sending a message to the swarm

When any of your applications want to send a message to the other nodes, just perform a HTTP POST to http://localhost:your_configured_port/communicate

Yes, http, not https. It only listens on interface "127.0.0.1" anyways for internal-only usage on the machine.

#### Receiving messages from other nodes

svc.js file has a function:

function onMessage(data) {}

"data" is the message. You are welcome ;)

Note: You will not receive your own messages, that you sent from that same machine. Everyone else will get it, but not you.

### Not a NodeJS developer? Fear not! We got you covered!

Check out our examples folder. We got two ( 2 ) examples there, one for http posting and one for tcp send, so you can forward the message to your own application and out of the NodeJS world. Just replace svc.js with any of the two from the examples folder. Enjoy!

Note: If you chose the http example, you must run "npm install" in that folder. package.json is configured already to download request, which that example uses. This means you need to download npm (comes with nodejs, pick latest LTS version).

This is not required for the tcp example, "net" package comes with nodejs, and our binary has a modified nodejs built-in.
