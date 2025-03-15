# PB-Compass-Atividade-Docker
 Este repositório contém exercícios sobre containers e Docker, abordando criação, gerenciamento e configuração de containers de forma prática e detalhada.


# 🐳 Programa de Bolsas DevSecOps 2025 – Módulo Docker  

Este repositório contém os exercícios práticos do módulo **Docker e Containers** do **Programa de Bolsas DevSecOps 2025**. Aqui, documentarei todo o processo, incluindo comandos utilizados, desafios encontrados e aprendizados adquiridos ao longo da atividade.  

## 📌 Sobre a atividade  

Este módulo é focado em entender os conceitos fundamentais de **Docker**, desde a criação de containers até sua manipulação e configuração. A atividade prática seguirá um **passo a passo** detalhado, cobrindo tópicos como:  

✔️ Criação e gerenciamento de containers  
✔️ Construção de imagens Docker  
✔️ Uso de Dockerfile  
✔️ Persistência de dados e volumes  
✔️ Networking entre containers  

Toda a documentação e código serão registrados aqui, permitindo que outras pessoas acompanhem e repliquem o aprendizado.  

##  Atividade Docker e Contêinerização

###  1. Criando o container Docker com a imagem do Nginx 🔧

Primeiro, criamos um container com a imagem oficial do **Nginx**, um servidor web popular.

```bash
docker run -dit --name meu-nginx -p 8080:80 nginx
```
### Criando uma página estática simples 🖥️
Criamos uma página HTML simples com conteúdo sobre o Programa de Bolsas 2025 e a Atividade de Docker. Os códigos estaram disponíveis aqui no github.

### Subindo a página no container 🛠️
Agora, subimos o arquivo index.html para o container para que o Nginx possa servi-lo:

```bash
docker run -dit --name meu-nginx -p 8080:80 -v ${PWD}/index.html:/usr/share/nginx/html/index.html nginx
```
Explicação:
- -v ${PWD}/index.html:/usr/share/nginx/html/index.html: Monta o arquivo HTML no diretório do Nginx dentro do container.

###  Acessando a página no navegador 🌐
Agora, basta acessar a página no navegador com o endereço: http://localhost:8080.
![pag](images/pag.png)


###   Personalizando a página
A página foi personalizada com Tailwind CSS e agora exibe informações sobre o Programa de Bolsas 2025 e a Atividade de Docker.

###   Resultado Final
Com isso, conseguimos criar um container Docker rodando o Nginx e servindo uma página estática com conteúdo personalizado. O processo foi simples, rápido e eficiente.

###  Conclusão 📝
Esta atividade demonstrou como utilizar o Docker para rodar um servidor Nginx em um container e servir uma página estática. O uso de Tailwind CSS ajudou a personalizar rapidamente a aparência da página.

## 2. Criando e rodando um container interativo
Inicialmente, foi criado um contêiner Ubuntu, que permite interagir diretamente com o terminal do sistema:
```bash
docker run -it ubuntu
```
### Atualização do sistema:
 Após iniciar o contêiner, o primeiro passo foi atualizar a lista de pacotes disponíveis, garantindo que o sistema estivesse com as últimas versões dos repositórios.

 ### Instalação do pacote **htop**:
  Em seguida, foi realizada a instalação do pacote htop, uma ferramenta que permite monitorar o uso do sistema em tempo real:
  ```bash
  apt install htop
  ```
  ### Execução do htop: 
  Após a instalação, o comando **htop** foi executado para verificar o funcionamento da ferramenta dentro do contêiner.
  
  ### Conclusão
  Esta atividade demonstra de maneira prática como utilizar Docker para criar contêineres e gerenciar pacotes dentro de um sistema Ubuntu. A utilização do **htop** também exemplifica como podemos interagir com o sistema e visualizar informações em tempo real de forma eficiente.

## 3. Listando e Removendo Containers no Docker
Essa atividade tem como objetivo ensinar a gerenciar containers no Docker, permitindo listar os containers em execução ou parados, além de demonstrar como parar e remover containers específicos. Esse processo é essencial para manter um ambiente Docker organizado, eliminando containers desnecessários e liberando recursos do sistema.
### Listar Containers
Para visualizar os containers em execução, use:
```bash
docker ps
```
Caso queira listar todos os containers (incluindo os que estão parados), utilize:
```bash
docker ps -a
```
### Parar um Container
Se houver um container em execução e for necessário pará-lo, use:
```bash
docker stop <CONTAINER_ID>
```
🔹 Substitua <CONTAINER_ID> pelo ID do container que deseja parar. Você pode obter esse ID usando o comando docker ps.

### Remover um Container
Para excluir um container específico, primeiro pare-o (se ainda estiver rodando) e depois remova-o com:
```bash
docker rm <CONTAINER_ID>
```
Se o container já estiver parado, basta rodar o comando acima.

🔹 Dica: Para remover vários containers de uma vez, liste os IDs e os remova:
```bash
docker rm $(docker ps -aq)
```
Isso apagará todos os containers parados.

## 4. Passo a Passo: Criando e Rodando um Container Docker para Aplicação Flask 📌 
Este guia explica como criar e rodar um container Docker para uma aplicação Flask, de forma simples e objetiva.

 ### Pré-requisitos 🛠️
 - Ter o Docker instalado em sua máquina.
 - Criar um diretório para sua aplicação.

### Estrutura do Projeto 📂
Antes de começar, sua pasta do projeto deve conter os seguintes arquivos:
```bash
minha-aplicacao/
│-- app.py
│-- requirements.txt
│-- Dockerfile
```
 ### Criar a Aplicação Flask 📌
Crie um arquivo app.py e adicione o seguinte código:
```bash
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Olá, mundo! Aplicação Flask rodando no Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```
🔹 Importante: O host='0.0.0.0' permite que o container seja acessado externamente.

 
### Criar o Arquivo requirements.txt 📌

Este arquivo lista as dependências do projeto. Adicione:
```bash
flask
```
Se houver mais bibliotecas, adicione uma por linha.

### Criar o Arquivo Dockerfile 📌

O Dockerfile define como a imagem Docker será construída. Adicione o seguinte conteúdo:
```bash
# Usando uma imagem oficial do Python
FROM python:3.9-slim

# Definindo o diretório de trabalho dentro do container
WORKDIR /app

# Copiando os arquivos para o container
COPY requirements.txt ./
COPY app.py ./

# Instalando as dependências
RUN pip install --no-cache-dir -r requirements.txt

# Expondo a porta 5000
EXPOSE 5000

# Comando para iniciar a aplicação
CMD ["python", "app.py"]
```
###  Construir a Imagem Docker 📌

Agora, no terminal (dentro da pasta do projeto), execute o comando:
```bash
docker build -t minha-aplicacao .
```
🔹 O -t minha-aplicacao dá um nome para a imagem.

### Rodar o Container
Agora que a imagem está pronta, rode o container:
```bash
docker run -p 5000:5000 minha-aplicacao
```
🔹 O -p 5000:5000 mapeia a porta do container para a máquina local.

### Acessar a Aplicação
Abra o navegador e acesse:
```bash
http://localhost:5000
```
