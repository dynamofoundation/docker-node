# Dynamo-Docker

This is a dockerized full node for DYNAMO coin. The intent for this project is to make running a full node more accessible for people to use for a dedicated mining node or contribute to the network.

Web-bridge & web wallet support has also been added although it is still being tested.


# Anatomy

```bash
.
├── README.md
├── TODO.MD
├── bridge                  <"Web Bridge" for node access>
│   ├── Dockerfile
│   └── settings.txt        <connection settings for bridge>
├── client.conf.example     <node client connection settings>
├── docker-compose.yml      <configuration for building the environment>
├── dynamo.conf.example     <full node settings>
├── node                    <the full node>
│   ├── Dockerfile
│   └── get-info.sh         <node info script>
├── php                     <php-fpm needed for the nginx web server>
│   ├── Dockerfile
│   └── bridge.php          <web bridge connection settings>
└── web
    ├── Dockerfile
    ├── bridge.php          <web bridge connection settings>
    └── site.conf           <nginx configuration>
```

# Summary of setup
(Note: This assumes a working docker environment already exists.)

    1. Create a location on disk where the node data will be stored.
    2. Edit the node/Dockerfile to use this as its volume. (Default is /var/tmp/dynamo)
    3. Create a dynamo.conf file based on the example and edit the user/password/nftdbkey settings.
    4. Place dynamo.conf file in your chosen data location.
    5. Edit the settings.txt in the bridge directory to match your user/password.
    6. (Optional) Create a client.conf based on the example and copy into your node data location.
    7. Run "docker-compose up" from the root project folder and environment will be built.
    8. BE PATIENT! The full node will need to sync from scratch as well as the web bridge. 
    9. Go to http://localhost to access the web wallet.

# Notes

"Bridge Troubleshooting"

* There is a verbose flag that can be enabled in the `settings.txt` file. These logs will be written to `log.txt` file inside the container so you will have to connect to it in order to see its contents.
* If your web bridge is crashing on sync, it likely isn't getting enough memory. This can be seen by running `docker stats` and looking at the "mem limit" which should be set to ~6Gb. (The bridge only needs this while syncing and will settle down to around 1.2G when done.) You may need to raise the memory limit for your core docker installation to allow for this. (I had to on my mac.)


If you need to re-build everything from scratch due to upstream code changes you can do the following:

```bash
docker-compose down --rmi all
docker-compose build --no-cache
docker-compose up
```

If you want to run the node image ONLY you have two options:

    1. Comment out the other services in the docker-compose.yml file
    2. Take the Dockerfile out of the node directory and follow the instructions in OLDREADME.MD


If you bothered to setup the client.conf file you can interact with the full node via the commandline client tool. The "get-info.sh" script is an example of this.

    1. Login to the container using a command like the example below:
        docker exec -it cc4899477f2f /bin/bash

    2. The client binary is named "dynamo-cli". You can run that or "get-info.sh". (Both are in /bin)



# Dev status

* Full node works.
* Web wallet works but NOT the BSC swap. (That functionality is not portable and only works on the foundation web wallet.)
* Updated for core node v1.1
