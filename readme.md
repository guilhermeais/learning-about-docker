# Aprendendo a utilizar Docker.
### O único objetivo deste repositório é aprender a utilizar e configurar Docker da maneira correta.
Basicamente tenho pouquíssimo conhecimento em Docker, e o objetivo deste repositório é tanto alavancar este conhecimento, quanto reunir informações que possam ser úteis a alguém.

<br/>

## Iniciando a criação do nosso Dockerfile

Após adicionarmos uma dependência a nossa aplicação (expressJS), e criarmos um mini-servidor.

Vamos criar um Dockerfile para controlarmos isso. 

Primeira coisa, é criarmos o Dockerfile (`touch Dockerfile`)

dentro dele, vamos colocar o seguinte:

``` 
/*
 FROM é qual máquina e qual versão vamos usar. Dizemos que vamos pegar o Node na sua última versão na versão alpine que é uma versão bem reduzida do Node
*/

FROM node:alpine

// Diretório dentro do Docker que vamos trabalhar
WORKDIR /usr/app

/*
 Copiamos tudo que é package*algumacoisa.json da nossa pasta para a raiz do docker (que é a WORKDIR)
*/
COPY package*.json ./
// E rodamos o npm install para baixar as dependências
RUN npm install 

/* 
  Depois copiamos todos arquivos restantes da nossa pasta para a workdir do docker

  E criamos a .dockerignore para ignorar o node_modules
*/
COPY . .

// Dizemos qual porta vamos expor nosso servidor no Docker
EXPOSE 3000

/*
E aqui passamos o comando para iniciar a nossa aplicação.

isso vai dependers de como configuramos a nossa package.json
*/
CMD ["npm", "start"]
```

Para buildarmos este arquivo Dockerfile que criamos, iremos usar o comando `docker build -t NOME_PARA_CONTAINER LOCAL_DO_DOCKERFILE`

Depois de buildar o nosso Dockerfile, precisamos rodar ele com o seguinte comando:
`docker run -p PORTA1:PORTA2 -d`

## (-p) Portas 
-p: Define as portas
PORTA1: Porta que vamos acessar no nosso navegador, por exemplo;
PORTA2: Quando acessarmos a PORTA1, vai redirecionar pra essa lá no Docker.

## (-d) imagem que vamos utilizar 
É o mesmo nome que demos ao container lá no docker build "NODE_PARA_CONTAINER"


### E pronto, temos nosso HELLO WORD e a aplicação toda rodando no Docker!! :D