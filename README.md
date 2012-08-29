# Developer Environment Setup

## Mac OS X Snow Leopard

### Step 1: Configure rndc

Create the rndc configuration file:

    rndc-confgen > /etc/rndc.conf

Create a keyfile that will allow the rndc client to talk to the name server and control it:

    head -n5 /etc/rndc.conf | tail -n4 > /etc/rndc.key

### Step 2: Enable BIND

Setup BIND to load up when your computer starts up:

    launchctl load -w /System/Library/LaunchDaemons/org.isc.named.plist

Start BIND:

    launchctl start org.isc.named

#### Step 3: Configure named

Backup the original rndc configuration file:

    cp /etc/named.conf /etc/named.conf.bak

Copy the custom named configuration file:

    cp named.conf /etc/named.conf

Copy the custom named zone file:

    cp local.zone /var/named/local.zone

#### Step 4: Validate the configuration

Make sure the named.conf file is setup properly use the built in tool checkconf:

    named-checkconf /etc/named.conf

Make sure the zone file is setup properly use checkzone:

    named-checkzone local /var/named/local.zone

#### Step 5: Reload the configuration

    rndc reload
    rndc flush
    dscacheutil -flushcache
