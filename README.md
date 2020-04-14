# How to use the nextcloud charm

This nextcloud server will default run on port 80.

Relate this charm with either mysql or postgresql.

### Example deploy
Below is a manual test deployment without SSL/TLS:
```
juju deploy cs:~erik-lonroth/nextcloud
juju deploy postgresql
juju relate postgresql:db nextcloud:postgres
juju expose nextcloud
```

### Example deploy of a bundle
The [nextcloud-collabora-tls bundle](https://jujucharms.com/u/erik-lonroth/nextcloud-collabora-tls/bundle/)
deploys a full collaboration office suite with [collabora online](https://www.collaboraoffice.com/)
with letsencrypt SSL certificates.

### Initial login
http://<trusted_domain>/

username: admin

password: mypassword

Change default passwords as soon as possible.

## Configuration
The charm has a few configuration variables you might want to set, depending on your needs. 

A reconfig will trigger a 'systemctl reload apache2'

- **fqdn**:

Set this if you have a DNS entry, E.g. nextcloud.example.com. You will avoid "untrusted domain" messages
in your browser with a valid domain name set here. 
```
juju config nextcloud fqdn=nextcloud.example.com
```

- **php_upload_max_filesize**:

Set this to a value reflecting the files you expect coming via the file sync. Default is 512MB.
```
juju config nextcloud php_upload_max_filesize="1G"
```
See the configuration (config.yaml) for more options.

## Actions
This charm provides the following actions that might be useful.

### action: add-trusted-domain
This action adds a trusted_domain through the nextcloud [occ] command.
```
juju run-action nextcloud/0 add-trusted-domain index=4 domain="nextcloud.my.local.domain"
```
The server will now accept requests via http://nextcloud.my.local.domain


## Installed version of Nextcloud
This charm installs a fairly recent release from [nextcloud releases] defined in the apache.yaml file.
If you need to install another version as part of your deploy - talk to the charm [Maintainer].

## Upgrading Nextcloud
Its safe to use the Nextcloud web-gui for normal operational upgrades. 
You find it in the "Overview" section in the deployed nextcloud.


# Paying me for work
I will update this charm on your explicit request in the [Github repo]. I'll accept payment in crypto.

 - bitcoincash:qzucec796gtey4qr4fg58rrd85zrlg5sw5pezeh6vs
 - bitcoin:1Hv6ngPnk7MDt5Gnxr6z6Pu7DgJiSKCTwR
 
 [Github repo]: https://github.com/erik78se/layer-nextcloud
 [Maintainer]: https://eriklonroth.com
 [nextcloud releases]: https://download.nextcloud.com/server/releases/
 [occ]: https://docs.nextcloud.com/server/16/admin_manual/configuration_server/occ_command.html