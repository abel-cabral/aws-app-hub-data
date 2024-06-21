Linux:
Ver Recursos de memoria disponivel:

````
free -h
````

Docker:

Limpar todos os caches e dados
````
docker stop $(docker ps -q) && docker rm $(docker ps -a -q) && docker rmi $(docker images -q) && docker system prune -a --volumes
````

Docker Stack

Deploy dos containers para o Cluster
````
docker stack deploy -c docker-compose.yml abelCluster
````


Interrompendo Serviços no Cluster
````
docker service ls
docker service rm servico1 servico2 servico3
````


NGINX

Reiniciar Servidor
````
sudo systemctl restart nginx
````


Certificados SSL

Instalacao:

````
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
````

Obter Certificados:
````
sudo certbot --nginx -d example.com
````

Renovacao automatica:
````
sudo certbot renew --dry-run
````
