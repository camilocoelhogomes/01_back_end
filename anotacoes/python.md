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