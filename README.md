
sudo cp /etc/named.conf /etc/named.conf.bak
sudo cp named.conf /etc/named.conf

sudo rndc-confgen | head -n5 > /etc/rndc.key

sudo cp local.zone /var/named/local.zone

