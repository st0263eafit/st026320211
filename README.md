Instalar docker en linux-ami2

    sudo amazon-linux-extras install docker
    sudo yum install git

    sudo systemctl enable docker
    sudo systemctl start docker
    sudo usermod -a -G docker ec2-user

instalar docker-compose: https://docs.docker.com/compose/install/

    sudo curl -L https://github.com/docker/compose/releases/download/1.28.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
 
    sudo chmod +x /usr/local/bin/docker-compose

    sudo reboot