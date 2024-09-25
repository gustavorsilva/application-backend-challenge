## Projeto backend-challenge: Validador de Tokens JWT com FastAPI
## Descrição
Este projeto é uma API desenvolvida com FastAPI para validar tokens JWT. A API verifica a estrutura e o conteúdo do token, garantindo que ele contenha exatamente três claims: Name, Role e Seed. Além disso, realiza validações específicas para cada claim, como o tamanho do nome de ate 256 caracteres e formato do Name no qual não pode ter números, a integridade do Role e a Seed no qual valida se é número Primo.
Recomendando esta na versão do Python 3.9 ou seperior [Link da biblioteca python](https://docs.python.org/3.9/)

## Instalação e Execução de aplicação

1 - Clone o Repositório:
```bash
git clone https://github.com/gustavorsilva/application-backend-challenge
cd application-backend-challenge
```
2 - Ambiente Linux:
```bash
cd application-backend-challenge/backendchallenge
```
execute os seguinte comandos:
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
```
## Uso
em seguida a aplicação esta disponivel no browser no endereço:
```bash 
Swagger UI
http://127.0.0.1:8000/docs
```
 ou prompt de comando:
 ```bash  
curl -X POST "http://127.0.0.1:8000/validate_token" \ -H "Content-Type: application/json" \ -d '{"token": "insira deu token"}'
```
tambem pode ser validado utlizando ferramentas como (insomnia ou postman).

2.1 - Ambiente Windows:
Recomendações: Instalação do Docker Desktop para execução do codigo.[Link para instalação do docker desktop](https://docs.docker.com/desktop/install/windows-install/)
Abra o arquivo com seu IDE de preferencia
```bash
cd application-backend-challenge/backendchallenge
```
Abra um terminal e execute os seguinte comandos:
Primeiro sera executado o build da aplicação
```bash
docker build -t jwt-api .
```
em seguida execute o comando sera montado a imagem no docker desktop:
```bash
docker run -d --name jwt-api -p 80:80 jwt-api 
```
## Uso
Com sua imagem ja sendo executado localmente, pode ser acessada localmente utilizando no browser no endereço:
```bash 
Swagger UI
http://127.0.0.1:80/docs
```
ou prompt de comando:
 ```bash  
curl -X POST "http://127.0.0.1:80/validate_token" \ -H "Content-Type: application/json" \ -d '{"token": "insira deu token"}'
```
tambem pode ser validado utlizando ferramentas como (insomnia ou postman).

## Como Utilizar localmente Insomnia ou outras ferramentas para execução de teste de api
- Insira o Curl completo na na URL clique em import, em seguida clique em send. Sua aplicação vai responder ao token
![Animação](https://github.com/user-attachments/assets/77b5fc61-e4ee-4e31-b842-d6af97d1b786)

## Endpoints da API
 ```bash
POST /validate_token
```
Valida um token JWT enviado no corpo da requisição.

Parâmetros
- Body: JSON contendo o token a ser validado.
```bash
{
  "token": "seu_token_jwt_aqui"
}
```
# Respostas
- 200 OK quanto para verdadeiro e falso o resto das informações estão no log da aplicação
```json
{
  "is_valid": "verdadeiro"
}
e
{
  "is_valid": "falso"
}
```
## Exemplo de Requisição Válida
```bash
curl -X POST "http://127.0.0.1:80/validate_token" \
-H "Content-Type: application/json" \
-d '{"token": "eyJhbGciOiJIUzI1NiJ9.eyJSb2xlIjoiQWRtaW4iLCJTZWVkIjoiNzg0MSIsIk5hbWUiOiJUb25pbmhvIEFyYXVqbyJ9.QY05sIjtrcJnP533kQNk8QXcaleJ1Q01jWY_ZzIZuAg"}'
```
- Resposta
```bash
{
  "is_valid": "verdadeiro"
}
```
- Log
![alt text](image.png)

## Exemplo de Requisição Invalida
```bash
curl -X POST "http://127.0.0.1:80/validate_token" \
-H "Content-Type: application/json" \
-d '{"token": "eyJhbGciOiJIUzI1NiJ9.eyJSb2xlIjoiTWVtYmVyIiwiT3JnIjoiQlIiLCJTZWVkIjoiMTQ2MjciLCJOYW1lIjoiVmFsZGlyIEFyYW5oYSJ9.cmrXV_Flm5mfdpfNUVopY_I2zeJUy4EZ4i3Fea98zvY"}'
```
- Resposta
```bash
{
  "is_valid": "falso"
}
```
- Log
![alt text](image-1.png)

