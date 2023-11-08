# Introdução

O pyhton será a linguagem de programação utilizada nesse módulo para o desenvolvimento back end

# Criação do ambiente

Para evitar que todas as dependências sejam instaladas de forma gloval, e evitar conflitos de dependencias entre diversos projetos é nescessário criar um ambiente virtual dentro do python, dessa forma é possível instalar as dependências nescessárias para determinado projeto, para a galera no node.js, simular ao node_modules

## 1. Criação do ambiente

```bash
python -m venv ./venv
```

## 2. Ativação do ambiente virtual

```bash
source venv/bin/activate
```

## 2. Desativação do ambiente virtual

```bash
deactivate
```

## 2. Instalação de pacotes

O gerenciador de pacotes do python é o pip para instalar um antes de tudo precisa garantir que um ambiente virtual esteja carregado e devidamente inicializado, conforme a seção anterior. após isso, basta realizar o comando conforme o exemplo mostrado a seguir com a instalação do django:

```bash
pip install django
```

## 3. Geração do arquivo de controle de dependências

Para gerar a lista de dependências do projeto, com todas elas instaladas, basta realizar o comando a seguir

```
pip freeze > requirements.txt
```

# Django

## 1. Inicialização do projeto

O comando a seguir deve ser rodado dentro da pasta do projeto desejado, ou seja, no mesmo nivel em que o ambiente virtual foi criado anteriormente. Dessa forma, ele irá criar uma pasta chamada setup, com todas as configurações dentro dessa mesma pasta

``` bash
django-admin startproject setup .
```

## 2. Inicialização do servidor django

1. Inclua o dominio **0.0.0.0** junto à variavel ALLOWED_HOSTS no comando no arquivo **./setup/settings.py**

```py
ALLOWED_HOSTS = ['0.0.0.0']
```

2. Rode o comando a seguir:

```bash
python manage.py runserver 0.0.0.0:8000
```

3. Caso desejar, pode alterar, junto ao settings.py vá até a seção de inicialização e faça as alterações nescessárias

4. Criação de um app

O comando a seguir é possível criar a estrutura básica para um dominio junto ao django

```bash
python manage.py startapp produto
```

5. Criação e aplicação das migrações no banco de dados

Sempre que um novo modelo for criado ou modificado, é de suma importância rodar as migrações nescessárias, já que isso indica uma alteração no modelo de dados do projeto

```bash
#Criação das migrations
python manage.py makemigrations

#Aplicação das migrations
python manage.py migrate
```

6. Criação de um novo modelo

Seguindo a sequência, dentro da pasta do app produto, existe um arquivo chamado models.py, cria uma classe python que extende um modelo do django, e que tenha as propriedades desse modelo

```py
from django.db import models

# Create your models here.
class Produto(models.Model):
  name = models.CharField(max_length=100)
  description = models.TextField()
  price = models.DecimalField(max_digits=10,decimal_places=2)
  category = models.CharField(max_length=10)
```
Rode os comandos de migração novamente

7. Criar um super usuário

```bash
python manage.py createsuperuser
```

8. Adicione o produto ao arquivo de admin.py

```py
from produto.models import Produto
# Register your models here.
admin.site.register(Produto)
```

9. Fazendo aparecer o nome do produto

Por padrão, na hora de listar o produto, o django chama o método **__str__()** da classe desejada, portnato se faz nescessário sobrescrever esse método, para que o mesmo retorno o nome do produdo

```py
from django.db import models

# Create your models here.
class Produto(models.Model):
  name = models.CharField(max_length=100)
  description = models.TextField()
  price = models.DecimalField(max_digits=10,decimal_places=2)
  category = models.CharField(max_length=10)

  def __str__(self) -> str:
    return self.name
```