#1. en una máquina AWS EC2 nueva y con la dirección IP Elastica de esa máquina, cree las entradas en el DNS:

    sudominio.com -> IP Elastica
    www.sudominio.com -> misma IP Elastica

#2. instale certbot:

    sudo amazon-linux-extras install epel -y
    sudo yum install certbot-nginx -y
    sudo yum install nginx -y

#3. Ejecute certbot para pedir certificado SSL:

    sudo certbot --nginx certonly -d www.sudominio.com -d sudominio.com

#4. cree el los archivos docker-compose

    mkdir /home/ec2-user/wordpress
    mkdir /home/ec2-user/wordpress/ssl
    sudo su
    cp /etc/letsencrypt/live/www.sudominio.com/* /home/ec2-user/wordpress/ssl/
    cp /etc/letsencrypt/options-ssl-nginx.conf /home/ec2-user/wordpress/ssl/
    cp /etc/letsencrypt/ssl-dhparams.pem /home/ec2-user/wordpress/ssl/
    exit

#5. instalar docker y docker-compose:

    sudo amazon-linux-extras install docker -y
    sudo yum install git -y
    sudo systemctl enable docker
    sudo systemctl start docker
    sudo usermod -a -G docker ec2-user
    sudo curl -L https://github.com/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    exit

#6. copie los archivos del docker al sitio propio e inicie

despues de clonar este repositorio en el destino:

    git clone https://github.com/st0263eafit/st026320211.git

    cd st026320211/docker-nginx-wordpress-ssl-letsencrypt
    sudo cp docker-compose.yml /home/ec2-user/wordpress
    sudo cp nginx.conf /home/ec2-user/wordpress
    sudo cp ssl.conf /home/ec2-user/wordpress

#7. inicie el servidor de wordpress en docker.

VERIFIQUE QUE NO ESTE CORRIENDO nginx NATIVO EN LA MÁQUINA, detengalo!!!!

    ps ax | grep nginx
    netstat -an | grep 80

    sudo reboot

vuelve y se conecta a la máquina para que ese proceso no esté corriendo.

UNA VEZ DETENIDO:

    cd /home/ec2-user/wordpress
    sudo docker-compose up --build -d

#8. pruebe desde un browser:

    https://sudominio.com o https://www.sudominio.com

#9.  FELICITACIONES, lo logro!!!!!
