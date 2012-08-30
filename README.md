# Developer Environment Setup

## Mac OS X Snow Leopard

### Step 1: Configure rndc

Create the rndc configuration file:

    sudo sh -c "rndc-confgen > /etc/rndc.conf"

Create a keyfile that will allow the rndc client to talk to the name server and control it:

    sudo sh -c "head -n5 /etc/rndc.conf | tail -n4 > /etc/rndc.key"

#### Step 2: Configure BIND

Backup the original rndc configuration file:

    sudo cp /etc/named.conf /etc/named.conf.bak

Copy the custom named configuration file:

    sudo cp bind/named.conf /etc/named.conf

Copy the custom named zone file:

    sudo cp bind/local.zone /var/named/local.zone

### Step 3: Enable BIND

Setup BIND to load up when your computer starts up:

    sudo launchctl load -w /System/Library/LaunchDaemons/org.isc.named.plist

Start BIND:

    sudo launchctl start org.isc.named

#### Step 4: Validate the configuration

Make sure the named.conf file is setup properly use the built in tool checkconf:

    named-checkconf /etc/named.conf

Make sure the zone file is setup properly use checkzone:

    named-checkzone local /var/named/local.zone

#### Step 5: Reload the configuration

    rndc reload
    rndc flush
    dscacheutil -flushcache

