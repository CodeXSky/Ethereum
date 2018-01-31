## systemd
### Go Ethereum As A Service

    $ more /etc/systemd/system/geth.service 
    [Unit]
    Description=Geth

    [Service]
    Type=simple
    User={user}
    # Environment={KEY}={VALUE}
    # EnvironmentFile=/home/user/.{service}.passwords
    Restart=always
    ExecStart=/usr/bin/geth --rpc

    [Install]
    WantedBy=default.target

And `/home/user/.{service}.passwords`

    KEY=VALUE

### systemd Commands

    # Reload the configuration
    $ sudo systemctl daemon-reload

    # Start / stop / restart
    $ sudo systemctl start {service}
    $ sudo systemctl stop {service}
    $ sudo systemctl restart {service}

    # View the logs
    $ sudo journalctl -u {service}

    # Tail the logs
    $ sudo journalctl -f -u {service}

## Bash 

* Command line editing using vi mode

        set -o vi

* Command line editing not using vi mode (which is the emacs mode)

        set -o emacs

## Install Let's Encrypt For Apache

    # Install Let's Encrypt client
    sudo apt-get update
    sudo apt-get install python-letsencrypt-apache
    
    # Set up SSL cert 
    sudo letsencrypt --apache -d example1.com -d www.example1.com -d example2.com -d www.example2.com
    
    # Auto renew - manually
    sudo letsencrypt renew
    
    # Auto renew 22:00 15th of every month
    sudo crontab -e
    0 22 15 * * /usr/bin/letsencrypt renew >> /var/log/le-renew.log

Test using https://www.ssllabs.com/ssltest/analyze.html?d=example.com&latest

Reference https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-16-04