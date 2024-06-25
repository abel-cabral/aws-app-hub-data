# Guia de Comandos Essenciais

Este guia contém comandos úteis para gerenciamento de recursos de memória no Linux, gerenciamento de containers Docker, manipulação de serviços Docker Stack, reinicialização do servidor NGINX e instalação e gerenciamento de certificados SSL. Basicamente dicas de como gerencias um "cluster" em uma instancia EC2 na AWS, permitindo ter varios serviços rodando na versão grátis (750 horas) da AWS.

## Índice
- [Linux](#linux)
  - [Ver Recursos de Memória Disponível](#ver-recursos-de-memória-disponível)
- [Docker](#docker)
  - [Limpar Todos os Caches e Dados](#limpar-todos-os-caches-e-dados)
  - [Comandos Básicos do Docker](#comandos-básicos-do-docker)
  - [Docker Stack](#docker-stack)
    - [Deploy dos Containers para o Cluster](#deploy-dos-containers-para-o-cluster)
    - [Interromper Serviços no Cluster](#interromper-serviços-no-cluster)
- [NGINX](#nginx)
  - [Reiniciar Servidor](#reiniciar-servidor)
- [Certificados SSL](#certificados-ssl)
  - [Instalação](#instalação)
  - [Obter Certificados](#obter-certificados)
  - [Renovação Automática](#renovação-automática)
- [Práticas Recomendadas](#práticas-recomendadas)

## Linux

### Ver Recursos de Memória Disponível
Para verificar a quantidade de memória disponível no sistema, utilize o comando abaixo:
```bash
free -h
```

## Docker

### Limpar Todos os Caches e Dados
Para parar todos os containers em execução, remover todos os containers, imagens e volumes do Docker, execute:
```bash
docker ps -q | xargs -r docker stop && \
docker ps -a -q | xargs -r docker rm && \
docker images -q | xargs -r docker rmi && \
docker volume ls -q | xargs -r docker volume rm && \
docker network ls -q | grep -v "bridge\|host\|none" | xargs -r docker network rm && \
docker system prune -a --volumes
```

### Comandos Básicos do Docker

Aqui estão alguns comandos básicos do Docker para gerenciamento diário:
•	Listar todos os containers em execução:
```bash
docker ps
```

•	Listar todos os containers (incluindo os que estão parados):
```bash
docker ps -a
```

•	Iniciar um container:
```bash
docker start <container_id>
```

•	Parar um container:
```bash
docker stop <container_id>
```

## Docker Stack

### Deploy dos Containers para o Cluster
Para fazer o deploy dos containers utilizando um arquivo docker-compose.yml para um cluster Docker Stack:
```bash
docker stack deploy -c docker-compose.yml abelCluster
```

### Interromper Serviços no Cluster
Para listar e remover serviços específicos em execução no cluster Docker:
```bash
docker service ls
docker service rm servico1 servico2 servico3
```

## NGINX

### Reiniciar Servidor
Para reiniciar o servidor NGINX, utilize o comando:
```bash
sudo systemctl restart nginx
```

## Certificados SSL

### Instalação
Para instalar o Certbot e o plugin NGINX, execute:
```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

### Obter Certificados
Para obter certificados SSL para o seu domínio utilizando o Certbot com NGINX:
```bash
sudo certbot --nginx -d example.com
```

### Renovação Automática
Para testar a renovação automática dos certificados SSL:
```bash
sudo certbot renew --dry-run
```

## Práticas Recomendadas

### Backup Regular
Certifique-se de realizar backups regulares dos seus dados e configurações. Use ferramentas como rsync para backups incrementais.

### Monitoramento de Sistema
Implemente ferramentas de monitoramento como Prometheus e Grafana para acompanhar o desempenho e a saúde do seu sistema e containers.

### Segurança
•	Firewall: Configure um firewall usando ufw ou iptables para restringir o acesso a serviços.

•	Atualizações: Mantenha seu sistema e pacotes sempre atualizados com sudo apt update && sudo apt upgrade.

### Documentação
Mantenha uma documentação detalhada de todos os processos e configurações para facilitar a manutenção e troubleshooting.
