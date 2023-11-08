# Criando o ambiente de desenvolvimento

Instale o Docker seguindo a documentação descrita em: <a href="https://www.docker.com/products/docker-desktop/">Docker</a>

# Dockerfile
O docker file tem por objetivo passar todas as informações nescessárias para criar uma imagem docker

Essa imagem servirá posteriormente de base para subir um novo container

## Estrutura

### FROM
```Docker
FROM python:3.12
```
Essa parte do código tem por objeti indicar qual será a imagem base a ser utilizada pela nossa imagem

### ENTRYPOINT

O comando ENTRYPOINT no Docker é usado para especificar o comando que será executado quando um contêiner baseado na imagem Docker for iniciado

```Docker
ENTRYPOINT ["tail", "-f", "/dev/null"]
```
Ele define o ponto de entrada do contêiner para ser o comando tail -f /dev/null. Aqui está uma explicação dos elementos:

1. ENTRYPOINT: É a instrução que define o comando que será executado quando o contêiner for iniciado. No seu caso, o comando é uma lista de argumentos, indicada por colchetes [].

2. **"tail"**: Este é o nome do programa que será executado. O tail é uma utilidade de linha de comando comum em sistemas Unix e Linux, geralmente usada para exibir as últimas linhas de um arquivo de registro ou outro arquivo de texto.

3. **"-f"**: Este é um argumento para o comando tail. Neste contexto, o argumento -f é usado para seguir (follow) o arquivo especificado. Isso significa que o tail continuará exibindo as linhas adicionadas ao arquivo em tempo real.

4. **"/dev/null"**: Este é o arquivo que o tail seguirá. No entanto, em um contexto Docker, seguir o /dev/null não tem um propósito real, pois o /dev/null é um dispositivo especial que descarta qualquer dado escrito nele. Portanto, seguir o /dev/null efetivamente não fará nada, e o contêiner não encerrará a execução enquanto estiver em execução.

Em resumo, esse comando Docker é um exemplo de um ponto de entrada que não faz nada de útil e mantém o contêiner em execução sem realizar nenhuma tarefa real. Pode ser usado em situações em que você deseja manter um contêiner em execução sem realizar nenhuma tarefa específica, mas ainda precisa que ele esteja ativo para outros fins, como redes ou testes.

## DockerCompose

O Docker compose facilita a criação dos containers nescessários ao ambiente de desenvolvimento podendo subir diversos container diferentes e diversas aplicações em paralelo

# Iniciando o ambiente de Desenvolvimento

O comando a seguir é utilizado para subir o ambiente de desenvolvimento

```bash
docker-compose up --build -d
```

O comando a cima irá subir o container, sua descrição é a seguinte

```yaml
version: "3.6"

services:
  api:
    build: ./src
    volumes:
      - ./aula:/aula
      - ./referencial:/referencial
    ports:
      - 8000:8000
      - 8080:8080

```

Onde na seção services serão definidos os seriços especificados

1. **api**: É o nome do serviço
2. **build**: É o caminho para o local em que o Docker file responsável por subir esse arquivo está
3. **volumes**: Realiza o mapeamento das pastas locais para pastas dentro do container
4. **ports**: Mapeias as portas para dentro do container

Junto com essas configurações, ao rodar o comando descrito no inicio dessa seção o Docker Compose criará um contêiner chamado "api" com as configurações especificadas. Ele será construído a partir do Dockerfile no diretório atual e terá acesso aos volumes mapeados para "/aula" e "/referencial". Além disso, as portas 8000 e 8080 do host estarão mapeadas para as portas correspondentes dentro do contêiner.