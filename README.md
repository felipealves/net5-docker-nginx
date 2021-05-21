# Exemplo de Web Api com Docker e Nginx

Para subir o sistema no docker basta seguir os seguintes passos:

  1. Clonar projeto;
  2. Ir no Wsl, ir até a pasta onde clonou o projeto;
  3. Criar uma rede NetWork no Docker
    3.1 docker network create --driver bridge {nomeRede}
  4. Executar o seguinte comando para criar o container da API de Test: docker build -f Webtest . 
    4.1: Executar o container da API utilizando a network criada:
      4.1.1: docker run -d -p 5000:80 --name Webtest --network {nomeRede}
      4.1.2: Realizar o comando para verificar o IP da API no Docker: docker inspect {containerAPI}
    4.2: Este Ip será necessário para configurar o Nginx;
  5. Na pasta do Nginx e alterar o arquivo 'nginx.conf', no parametro 'proxy_pass' informando o {IP do Container da API}:5000
  6. Executar o comando para criar a imagem do Nginx: docker build -f nginx . 
  7. Executar o container do Nginx:
    7.1: docker run -d -p 3000:80 --name nginx --network {nomeRede}
  8. Verificar se os container estão rodando certinho: docker ps
  9. Só testar no browser chamando por 'https:localhost:3000/swagger'
   ...EM construção e testes
