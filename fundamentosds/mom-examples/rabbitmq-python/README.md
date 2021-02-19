lanzar un servidor RabbitMQ en docker para estos ejemplos:

tutorial de: https://medium.com/better-programming/introduction-to-message-queue-with-rabbitmq-python-639e397cb668

    $ docker run -d --hostname my-rabbit -p 15672:15672 -p 5672:5672 --name rabbit-server -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password rabbitmq:3-management