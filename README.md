# Atividade: Fundamentos e Prática com Microsserviços  
### 1. Explique com suas palavras o que caracteriza uma arquitetura de microsserviços.  
**Resposta:** Arquitetura de microsserviços se basea-se em dividir o sistemas em pequenas funcionalidades que se comunicam entre si.  
### 2. Compare os modelos monolítico e de microsserviços, destacando pelo menos 3 vantagens e 2 desvantagens dos microsserviços.
#### Vantagens
- Escalabilidade independente, já que consegue melhorar partes do sistema
- Facilidade nas manutenções, pois já que é separado em pequenas partes os ajustes tornam-se mais facil já que cada ponto é extramamente especifico para cada operação
- Maior consistência na atividade do sistema, já que caso um serviço pare de funcionar o sistema continue operando
#### Desvantagens
- Custo operacional, já que pode exigir um infraestrutura mais robusta
- Complexidade no Gerenciamento, exigência mais precisa na comunicação entre os serviços
  
### 3. Considere o seguinte cenário de sistema:
Uma plataforma de ensino online com funcionalidades de:  
```CMD
● Autenticação de usuários  
● Catálogo de cursos  
● Vídeo-aulas  
● Emissão de certificados  
● Suporte ao aluno
```
Liste pelo menos 4 possíveis microsserviços e justifique a separação.  
- Microserviço: Gerenciação de login do usuário  
- Microserviço: Cadastro do usuário  
- Microserviço: Autenticação do usuário via token  
- Microserviço: Autorização do acesso de acesso por perfil do usuário

**Resposta:**  Justificativa: pois separar as responsabilidade do serviço ajuda a facilitar a manutenbilidade e escalibilidade do serviço
### 4. Cite e explique duas formas de comunicação e quando cada uma é mais indicada.  
- Comunicação Síncrona: **HTTP/REST**  
Explicação: Um microsserviço faz uma requisição direta para outro e aguarda a resposta antes de continuar o processamento.  

- Comunicação Assíncrona: **RabbitMQ, Kafka**  
Explicação: Um microsserviço envia uma mensagem para uma fila, e outro serviço processa essa mensagem de forma independente, sem que o primeiro espere a resposta.  
### 5. Você possui um microsserviço em Node.js com um Dockerfile.  
Escreva os comandos para:  
a) Criar a imagem com o nome pedido-service.  
```Dockerfile
FROM node                                  
WORKDIR /app                                          
COPY package*.json ./                                  
RUN npm install
COPY . .            
CMD["npm", "run", "start:dev"]
```

```CMD
docker build -t pedido-service .
```
b) Executar o container mapeando a porta 3000 do container para a porta 8080 da máquina host.  
```CMD
docker run -d -p 8080:3000 --name pedido-service pedido-service
```
### 6. Em uma arquitetura baseada em microsserviços, é recomendado que cada serviço tenha seu próprio banco de dados? Por quê?
**Resposta:** É recomendado que cada microsserviço tenha seu próprio banco de dados. Isso acontece porque cada serviço é responsável por seu próprio domínio de dados e deve ser independente dos demais. Ter bancos de dados separados evita que os serviços fiquem acoplados, permitindo que cada um evolua, escale e seja mantido de forma isolada. Além disso, essa separação ajuda a garantir a autonomia de desenvolvimento e implantação dos microsserviços, facilitando a manutenção e a resiliência da arquitetura. Para comunicação entre serviços, geralmente são usados APIs ou mecanismos de mensageria, em vez de acessar diretamente o banco de dados de outro serviço, o que evita dependências diretas e promove um design desacoplado.



# Atividade: Fundamentos e Prática com Docker    
### 1. O que é Docker e qual problema ele resolve no desenvolvimento e implantação de aplicações?  
**Resposta:** Docker é uma plataforma que permite empacotar aplicações e suas dependências em containers, garantindo que funcionem da mesma forma em qualquer ambiente. Ele resolve o problema de diferenças entre ambientes de desenvolvimento e produção, evitando o erro "na minha máquina funciona". Também facilita o deploy, pois a aplicação é executada dentro de um ambiente padronizado e isolado.  
### 2. Qual comando Docker você utilizaria para:
a) Listar todas as imagens Docker disponíveis localmente:  
```CMD
docker images
```  
b) Ver os containers em execução:  
```CMD
docker ps
```` 
c) Parar um container com ID abc123  
```CMD
docker stop abc123
```
d) Remover uma imagem chamada meu-app:latest  
```CMD
docker rmi meu-app:latest
```
### 3. Dada a imagem oficial do NGINX, escreva o comando completo para rodar um container em segundo plano (modo detached), mapeando a porta 80 do container para a 8080 do host, com o nome meu-nginx.  
```CMD
docker run -d -p 8080:80 --name meu-nginx nginx
```
### 4. Considere o seguinte Dockerfile:  
```Dockerfile
FROM python:3.10                                      // Baixa uma imagem do docker hub
WORKDIR /app                                          // Serve para definir o diretório de trabalho dentro de um contêiner Docker
COPY ...                                              // Copia o diretório
RUN pip install -r requirements.txt                   // Instala todas as dependencias da apliação
CMD["python", "app.py"]                               // Executa o programa
```


### 5. Você possui um projeto em uma pasta chamada meu-projeto com um Dockerfile.  
Quais comandos você executaria para:  
a) Construir a imagem com o nome meu-projeto:1.0  
```CMD
docker build -t meu-projeto:1.0 .
```
b) Executar essa imagem em um container  
```CMD
docker run meu-projeto:1.0
```
### 6. Considere o seguinte docker-compose.yml:  
```docker-compose.yml
version: '3'
	services:
	 web:
	  build: .
	  ports:
	   -"5000:5000"
	 redis:
	  image: redis
```
a) Quantos serviços estão definidos?  
**Resposta:** 2  
b) Qual porta será exposta pela aplicação web?  
**Resposta:** A porta vai ser 5000  
