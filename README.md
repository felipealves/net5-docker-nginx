# Exemplo de publicação de uma Web Api com Docker e Nginx

Para subir o sistema no docker basta seguir os seguintes passos:

  Clonar projeto;  
  Ir no Wsl, ir até a pasta onde clonou o projeto;  
  Criar uma rede NetWork no Docker;  
> docker network create --driver bridge {nomeRede}  

  Ir até a pasta do WebTest na linha de comando e executar o seguinte comando para criar a imagem da API de Test:
> docker build -t webtest .

  Caso queira verificar se criou tudo certo só executar o comando:  
> docker images

  Executar o container da API utilizando a network criada: 
> docker run -d -p 5000:5000 --name {nomeContainer} --network {nomeRede} webtest

  Realizar o comando para verificar o IP da API no Docker:  
> docker inspect {containerAPI} 


  Este "IPAddress" será necessário para configurar o Nginx;  
  Na pasta do Nginx e alterar o arquivo 'nginx.conf', no parametro 'proxy_pass' informando o {IP do Container da API}:5000  
  Ir até a pasta do Nginx na linha de comando e Executar o comando para criar a imagem do Nginx:  
> docker build -t nginx-webtest .


  Executar o container do Nginx:  
> docker run -d -p 3000:80 --name {nameContainer} --network {nomeRede} nginx-webtest


  Verificar se os container estão rodando certinho:  
> docker ps


  Só testar no browser chamando por **https:localhost:3000/swagger**
