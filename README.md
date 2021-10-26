# README

## Antes de instalar

1. Algunas gemas necesarias para Simple Project Management App **no son** compatibles con Windows. Por favor, intenta usar Linux o MacOS.
2. Esta instalación asume que has clonado este repositorio.

## Requisitos adicionales

Las siguientes dependencias son necesarias y deben ser instaladas antes de la instalación de la aplicación:

| Dependencia | Version | Instalación |
|---|---|---|
| PostgreSQL | 11 | [For Debian and related versions][5] |
| Rbenv | latest | See below |
| Ruby | 2.6.3 | See below |
| NVM | latest | [Instructions][6] |
| Node.js (with NVM) | 14 LTS | See [above][6] |
| Yarn | latest | See below |

Después de instalar PostgreSQL, y para poder ser utilizado desde Ruby, es necesario configurar un superusuario (además del rol `postgres`). Se recomienda utilizar el mismo nombre de usuario de su máquina. Ejecute lo siguiente:

```sh
sudo -u postgres -i
psql
CREATE ROLE <user> WITH LOGIN PASSWORD '<password>';
ALTER ROLE <user> WITH SUPERUSER;
```

## Instalación de Rbenv y Ruby

Rbenv te permite instalar y gestionar las versiones de Ruby fácilmente.

Primero, asegúrate de que tienes todas las dependencias necesarias:
```sh
sudo apt update

sudo apt install -y curl gnupg2 dirmngr git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev libpq-dev imagemagick
```

A continuación, para instalar Rbenv en su sistema, ejecute los siguientes comandos:
```sh
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
```

El plugin de Rbenv `ruby-build` simplifica la instalación de nuevas versiones de Ruby. Por lo tanto, necesitas ejecutar los siguientes comandos:
```sh
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```

A continuación, puedes instalar Ruby:
```sh
rbenv install 2.6.3
```

El comando anterior puede ser lento. Por favor, ten paciencia.

Una vez finalizado, necesitas configurar esto como versión global en todos los entornos de Ruby:
```sh
rbenv global 2.6.3
```

Después de esto, puedes comprobar si Ruby fue instalado con éxito con el comando `ruby -v`

## Instalación de Yarn

El paquete Yarn está disponible en el repositorio Yarn. Ejecute los siguientes comandos para importar la clave GPG del repositorio y habilitar el repositorio APT:
```sh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

Una vez habilitado el repositorio, actualiza el índice de paquetes e instala Yarn:
```sh
sudo apt update
sudo apt install --no-install-recommends yarn
```

Verifica la instalación imprimiendo el número de versión de Yarn: `yarn --version`

## Instalación de simple-project-management-app

1. Instalar bundler:
```sh
gem install bundler
```

2. Ve a la carpeta de tu repositorio clonado:
```sh
cd <ruta_del_repositorio>/simple-project-management-app
```

3. Instala las gemas:
```sh
bundle install
```

Esto tomará algún tiempo. Tenga paciencia.

4. Instala las dependencias de Node.js:
```sh
yarn install
```

5. Create databases and models on PostgreSQL:
```sh
rails db:create
rails db:migrate
```

Finalmente, puedes ejecutar la aplicación con el siguiente comando: `rails s`. Para un desarrollo más rápido en las vistas de Javascript se recomienda ejecutar también `bin/webpack-dev-server` en otro terminal.

Ya está.
