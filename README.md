# Relatório Infraestrutura de Sistemas Web
Relatório de instalação e configuração CMS Wordpress e AVA Moodle usando LAMP - Linux, Apache, MySQL e PHP.

## Wordpress
### Instalação
Instale e configure os serviços LAMP:
* Apache 2;
* MySQL;

Após a finalização da instalação do MyWQL e preciso logar no Banco de Dados com um usuário com privilégios, como por exemplo:

`mysql -u root -p`
  
Depois de entrar com o password crie um banco de dados separado para o WordPress, o exemplo abaixo cria um BD de nome WordPressDB: 

`mysql> CREATE DATABASE WordPressDB DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;`

Quando finalizar saia do prompt do MySQL.<br>
Para a instalação do Wordpress propriamente dita, crie um arquivo de configuração: __WordPress.conf__ no diretório __/etc/apache2/sites-available/__.<br>
No arquivo *WordPress.conf* você pode habilitar .htaccess adicionando estas linhas ao bloco VirtualHost:

`<Directory /var/www/wordpress />`<br>

>`AllowOverride All`<br>

`</Directory>`

Crie o diretório WordPress no diretório __/var/www/wordpress__.<br>
Salve o arquivo e depois reinicie o servidor Apache usando o comando:

`sudo systemctl restart apache2`

Acesse o diretório __/var/www/wordpress__ e baixe o arquivo do Wordpress:

`curl -O https://wordpress.org/latest.tar.gz`

Extraia este arquivo usando:

`tar xzvf latest.tar.gz`

Crie o arquivo .htaccess:

`vi /var/www/wordpress/.htaccess`

Salve o arquivo. Troque o nome do arquivo wp-config-sample.php usando o comando:

`mv /var/www/wordpress/wp-config-sample.php /var/www/wordpress/wp-config.php`

Crie a pasta abaixo no local indicado:

`mkdir /var/www/wordpress/wp-content/upgrade`

Para a configuração inicial, é necessário gerar o salt do WordPress. Isso pode ser feito usando:

`curl -s https://api.wordpress.org/secret-key/1.1/salt/`

Ele dará uma saída diferente a cada vez e conterá uma lista de valores salt. A saída do comando acima precisa ser copiada e adicionada ao arquivo wp-config.php.

`vi /var/www/wordpress/wp-config.php`

Substitua os valores fictícios existentes nesse arquivo. Salve o arquivo depois de fazer as alterações.<br>

O arquivo wp-config.php contém algumas configurações do banco de dados no topo. Substitua o DB_NAME, DB_USER, DB_PASSWORD pelos valores que você criou para o WordPress.

`define('DB_NAME', 'WordPressDB' `

`/** MySQL database username */`

`define('DB_USER', 'WordPressUser');`

`/** MySQL database password */`

`define('DB_PASSWORD', 'DB_Password');`

Além disso, você pode adicionar o método do sistema de arquivos na parte inferior, conforme mostrado abaixo:

`define('FS_METHOD', 'direct');`

Salve o arquivo.<br>
Acesse o arquivo com:

`http://seuIP/wordpress`
  
### Configuração


## Moodle
### Instalação


### Configuração
