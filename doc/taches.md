# Taches à réaliser

* ssh client depuis windows (PUTTY) avec exchange le clé ssh(zohari)
* ssh au dessus de proxy HTTP(zohari)
* connection VNC au Linux(legrand)
	* reverse vnc
* connection VNC sur Windows(canivez)
* VNC au dessus de ssh



### ssh au dessus de proxy HTTP

#### Installation corkscrew

introduction
------------
Corkscrew est un outil de tunnelling SSH via les proxys HTTP.

Pour le construire, vous devez le télécharger, puis,  dans
le répertoire de corkscrew, tapez './configure' puis 'make'.

Pour l'installer dans le répertoire du corkscrew, tapez 'make install'.


Comment est-il utilisé?
---------------
La mise en place decorkscrew avec SSH / OpenSSH est très simple. Ajouter
La ligne suivante dans le fichier ~ / .ssh / config :

```javascript
Host *
   ProxyCommand /tmp/toto/bin/corkscrew cache-etu.univ-lille1.fr 3128 %h %p 
```

Remplacer /tmp/toto/bin/corkscrew cache-etu.univ-lille1.fr et 3128 par des valeurs correctes


##### mon problème vient de la connection au serveur avec ssh:

malgré que la clé ssh soit correcte, je reçoie ce message d'erreur 


```javascript
ssh -vvv cgir@test.boulgour.com
OpenSSH_6.7p1 Debian-5+deb8u3, OpenSSL 1.0.1t  3 May 2016
debug1: Reading configuration data /home/infoetu/zoharif/.ssh/config
debug1: /home/infoetu/zoharif/.ssh/config line 5: Applying options for *
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: Applying options for *
debug1: Executing proxy command: exec /tmp/toto/bin/corkscrew cache-etu.univ-lille1.fr 3128 test.boulgour.com 22
debug1: permanently_drop_suid: 1779
debug1: identity file /home/infoetu/zoharif/.ssh/id_rsa type 1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_rsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_dsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_dsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_ecdsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_ecdsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_ed25519 type -1
debug1: key_load_public: No such file or directory
debug1: identity file /home/infoetu/zoharif/.ssh/id_ed25519-cert type -1
debug1: Enabling compatibility mode for protocol 2.0
debug1: Local version string SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u3
Proxy could not open connnection to test.boulgour.com:  Forbidden
ssh_exchange_identification: Connection closed by remote host
```

je trouve que corkscrew peut être utilisé pour se connecter à un serveur SSH exécuté sur un port 443 distant via un proxy HTTPS strict.donc je pense le seul moyen pour resoudre ce problème est de changer le port ssh sur le serveur distant.



