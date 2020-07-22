# Deploy de um Projeto Django no HEROKU
## Este é um guia para quem já tem um projeto Django e deseja colocá-lo em produção. 

## Preparação do ambiente

* Atualizar pip `pip install --upgrade pip`
* Instalar dependencias `pip install django django-cors-headers django-extensions django-filter django-jet django-rest-auth djangorestframework dj-database-url dj-static python-decouple gunicorn psycopg2`

### Detalhando as dependências
* **django**: Framework para desenvolvimento web
* **django-cors-headers**: Módulo para permitir acesso via cors (cross domain origin)
* **django-extensions**: *dev*. Ativa extenções para desenvolvedor
* **django-filter**: Módulo para utilizar filtros no django
* **django-jet**: Template para o admin
* **django-rest-auth**: Módulo para autenticação via REST
* **djangorestframework**: Módulo para desenvolver apis REST
* **dj-database-url**: Módulo para converter string de conexão em url
* **dj-static**: Módulo para servir arquivos staticos
* **python-decouple**: Módulo que ajuda na parte de seguraça da aplicação (utilizar parametros via arquivo .env)
* **gunicorn**: Servidor web
* **psycopg2**: Módulo de acesso ao postgres

## Configurando o projeto

Primeiro, vamos salvar os módulos que nosso projeto necessita:  
`pip freeze > requirements.txt`



Agora iremos efetuar algumas configurações:

Primeiro, vamos ao arquivo `settings.py`. Nele, iremos informar as chaves do projeto, conexão de banco de dados, caminhos, etc.

Para aumentar a segurança, e remover desse arquivo dados de senha e chave, vamos utilizar o decouple. Para isso vamos criar o arquivo `.env`

Nele vamos informar os seguintes itens:

```
SECRET_KEY=Copiar chave secreta do seu settings.py
DEBUG=True
```

Agora dentro do nosso `setting.py`, vamos efetuar os imports do decouple e dj-database-url, logo após o `import os`:

```python
from decouple import config
from dj_database_url import parse as dburl
```

Agora vamos configurar nossas variáveis `SECRET_KEY` e `DEBUG` para obter as informações do arquivo `.env`

```python
# arquivo settings.py
SECRET_KEY = config('SECRET_KEY')

DEBUG = DEBUG = config('DEBUG', default=False, cast=bool)
```

Em desenvolvimento, vamos usar o `sqlite`, então para configurá-lo, vamos criar uma variável, passando o valor padrão para caso não houver informações de conexão no arquivo

```python
# arquivo settings.py

default_db_url = 'sqlite:///' + os.path.join(BASE_DIR, 'db.sqlite3')
```

A nossa string de conexão, irá ficar dessa forma:

```python
# arquivo settings.py

DATABASES = {
    'default': config('DATABASE_URL', default=default_db_url, cast=dburl)
}
```

Agora vamos efetuar algumas outras configurações importantes como hosts permitidos para acessar, linguagem, timezone, local dos arquivos staticos e etc.

```python
# hosts
ALLOWED_HOSTS = [
    '*'
]
# tradução
LANGUAGE_CODE = 'pt-br'
# timestamp
TIME_ZONE = 'America/Cuiaba'
# desativa timezone
USE_TZ = False
# diretorio de arquivos staticos
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```

Feito isso, vamos adicionar algumas estruturas do HEROKU (aws):

Para isso, vamos precisar criar o app no heroku, criar os arquivos Procfile, runtime.txt.

Primeiro, precisamos informar quem vai servir os arquivos staticos no heroku, por isso utilizamos o módulo `dj-static`. Para isso, abra o arquivo `wsgi.py`:

```python
import os
from dj_static import Cling

from django.core.wsgi import get_wsgi_application

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "atividades.settings")

application = Cling(get_wsgi_application())
```

Agora, vamos criar o arquivo `Procfile`, que informa ao heroku como que as coisas vão acontecer:

```
web: gunicorn nomeprojeto.wsgi
web: python manage.py runserver 0.0.0.0:$PORT
```

Agora, camos criar o arquivo `runtime.txt`, que informa qual versão do python vamos utilizar:

```
python-3.8.2
```

Feito isso, vamos preparar o git.

Primeiro, iniciamos o repositório com o comando `git init` e depois vamos criar o arquivo `.gitignore`, para não enviarmos alguns arquivos.

```git
.DS_Store
.env
.idea
.venv
*.sqlite3
*pyc
__pycache__
```

Feito isso, vamos comitar os arquivos. Primeiro enviamos o .gitignore

```git
git add .gitignore
git commit -m "Add ignore config"
```

Agora vamos enviar os arquivos de configuração do heroku

```git
git add Procfile runtime.txt
git commit -m "Heroku config"
```
Agora vamos enviar os arquivos de migrações do banco
* Obs: Antes de fizer isso rode as migrações localmente com ```python manage.py makemigrations && python manage.py migrate```

```git
git add nome-do-projeto/migrations/*.py -f
git commit -m "Migration config"
```
Agora, vamos importar o restante dos arquivos

```
git add .
git commit -m "Import project"
```

Agora, vamos ao Heroku.

Nessa etapa, precisamos criar o app, configurar as variaveis, e enviar os arquivos.

Antes de começar, instale o heroku client para utilizar os comandos.

Vamos criar e configurar o app:

```bash
heroku create nomeprojeto --buildpack heroku/python
heroku addons:create heroku-postgresql:hobby-dev
heroku pg:promote DATABASE_URL
heroku plugins:install heroku-config
heroku config:push
```

Feito isso, vamos enviar o projeto

```
git push heroku master
```

Pronto, projeto no ar!!!



Após isso, vamos rodar as migrações e criar o usuario admin:

```
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

## Créditos
* Este guia teve como base no tutorial do William Galleti [clique aqui para acessar o tutorial](http://wgalleti.io/desenvolvimento/pythondjango/heroku/) .