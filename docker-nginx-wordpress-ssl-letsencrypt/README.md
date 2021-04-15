1. en una máquina AWS EC2 nueva:
2. con la dirección IP Elastica de esa máquina, cree las entradas en el DNS:

    sudominio.com -> IP Elastica
    www.sudominio.com -> misma IP Elastica

2. instale certbot:

    sudo amazon-linux-extras install epel -y
    sudo yum install certbot-nginx -y
    sudo yum install nginx -y

3. Ejecute certbot para pedir certificado SSL:

    sudo certbot --nginx certonly -d www.sudominio.com -d sudominio.com

4. cree el los archivos docker-compose

    mkdir $HOME/wordpress
    mkdir $HOME/wordpress/ssl
    sudo cp /etc/letsencrypt/live/www.emontoya.ml/* $HOME/wordpress/ssl/
    sudo cp /etc/letsencrypt/options-ssl-nginx.conf $HOME/wordpress/ssl/
    sudo cp /etc/letsencrypt/ssl-dhparams.pem $HOME/wordpress/ssl/

5. instalar docker y docker-compose:

    sudo amazon-linux-extras install docker -y
    sudo yum install git -y
    sudo systemctl enable docker
    sudo systemctl start docker
    sudo usermod -a -G docker ec2-user
    sudo curl -L https://github.com/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    exit