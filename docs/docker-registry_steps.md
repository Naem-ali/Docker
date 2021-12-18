Connect to a private docker registry with HTTPS configured or without

add this to /etc/docker/daemon.json

{
  "insecure-registries": ["<IP>:<PORT>"]
}

afterwards restart docker service

sudo systemctl restart docker


Private docker registry
  1. you can also insert the command in cli to start the registry container,
     $ docker run -d -p 5000:5000 --restart=always --name registry registry:2

Private docker REgistry with TLS
  1. cretae a self signed TLS certificate
     mkdir /root/certs && cd /root/certs
  2. create a certificate
     openssl req -new -newkey rsa:4096 -x509 -sha256 -days 365 -nodes -out domain.crt -keyout domain.key
  3. Restrict the key permission so that only root can access.
     chmod 400 /root/certs/domain.key
  4. Back up your certificateto the external storage

Private docker registry with TLS and AUTH
  1. create a htpasswd and saves in auth, following command creates a file and stores a record in it for test_user
     ex. htpasswd -c /home/auth/ .htpasswd test_user
     after this user is prompted for a password.








