# nidulus_swarm
Nidulus MESH Swarm Controller

## Connecting the world

This neat little application will put all your machines/devices who share the same network in a shared MESH Swarm.
Sending data to all other nodes on the network is as easy as doing a HTTP POST to http://localhost:<your_configured_port>
Originally created for quick syncing of data between devices.

### Prerequisites
Linux x64

### Description of nidulus_swarm

When you download and unzip the package you will find three ( 3 ) important files.

nidulus_swam:         The application
config/settings.json: The configuration
svc.js:               The file containing onMessage function which is executed each time another node sent a message

### Getting started

1: Place the package on all machines/devices you want to swarm
2: Unpack (duh)
3: Edit the config/settings.json file (see below)
4: Start the nidulus_swarm
5: Use it (see below)

### Configuring

#### Threads

Decide how many threads you want the app to run in. Higher value = higher throughput. Each receiver will still get 1x copy of each message, don't worry. No multiplying messages, just more juice.

It is useless to set a higher threads count than you actually have physical cpu cores (no, virtual doesn't count). This will slow the throughput rather than increase it. Note that nidulus_swarm is written in NodeJS, meaning it does a lot of async even on one core and is fast. You might not need to increase this for your use-case.
