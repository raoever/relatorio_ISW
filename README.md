# Relatório Infraestrutura de Sistemas Web
Relatório de instalação e configuração CMS Wordpress e AVA Moodle usando LAMP - Linux, Apache, MySQL e PHP.

## Wordpress
### Instalação
Instale e configure os serviços LAMP:
* Apache 2;
* MySQL;

Após a finalização da instalação do MySQL e preciso logar com um usuário que tenha privilégios, como por exemplo:

`mysql -u root -p`
  
Depois de entrar com o password crie um banco de dados separado para o WordPress, o exemplo abaixo cria um BD de nome WordPressDB: 

`mysql> CREATE DATABASE WordPressDB DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;`

Quando finalizar saia do prompt do MySQL.<br>
Para a instalação do Wordpress propriamente dita, crie um arquivo de configuração: __WordPress.conf__ no diretório __/etc/apache2/sites-available/__.<br>
No arquivo *WordPress.conf* você pode habilitar .htaccess adicionando estas linhas ao bloco VirtualHost:

`<Directory /var/www/wordpress />`<br>

>`AllowOverride All`<br>

`</Directory>`

Salve o arquivo.<br>
Depois reinicie o servidor Apache usando o comando:

`sudo systemctl restart apache2`

Crie o diretório para o WordPress: __/var/www/wordpress__.<br>
Acesse o diretório __/var/www/wordpress__ e baixe os arquivos do Wordpress:

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
Acesse em um browser a URL:

`http://ipDoSeuServidor/wordpress`

Escolha a linguagem de sua preferência.<br>

![Linguagem](https://github.com/raoever/relatorio_ISW/blob/main/wordpress/wordpress1.png)

Digite o título do site, o nome do usuário, uma senha e um e-mail.<br>
Depois pressione o botão __Instalar WordPress__

![Informações básicas](https://github.com/raoever/relatorio_ISW/blob/main/wordpress/wordpress2.png)

Então aparecerá uma tela confirmando a instalação do WordPress e o usuário com a senha escondida.<br>
Pressione o botão __Acessar__ para ir para o login que dá acesso ao painel de controle.

![Sucesso](https://github.com/raoever/relatorio_ISW/blob/main/wordpress/wordpress3.png)

A tela de login será carregada.

![Login](https://github.com/raoever/relatorio_ISW/blob/main/wordpress/wordpress4.png)

E então a tela do Painel.

![Painel WordPress](https://github.com/raoever/relatorio_ISW/blob/main/wordpress/wordpress5.png)

<br><br><br>
## Moodle
### Instalação
Instale e configure os serviços LAMP:
* Apache 2;
* MySQL;
* PHP

Após a finalização da instalação do MySQL e preciso logar com um usuário que tenha privilégios, como por exemplo:

`mysql -u root -p`
  
Depois de entrar com o password crie um banco de dados separado para o Moodle, o exemplo abaixo cria um BD de nome MoodleDB: 

`mysql> CREATE DATABASE MoodleDB DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;`

Quando finalizar saia do prompt do MySQL.<br>
Depois reinicie o servidor Apache usando o comando:

`sudo systemctl restart apache2`

Crie o diretório para o Moodle: __/var/www/moodle__.<br>
Acesse o diretório __/var/www/moodle__ e baixe os arquivos do Moodle:

`wget https://download.moodle.org/stable38/moodle-latest-38.tgz`

Descompacte:

`tar -zxvf moodle-latest-38.tgz`

Crie o diretório para o Moodle: __/var/www/moodledata__.<br>

### Configuração
Acesse em um browser a URL:

`http://ipDoSeuServidor/moodle`

Escolha a linguagem de sua preferência.

![Linguagem](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle1.png)

Confirme os caminhos do Endereço web, Diretório Moodle e Diretório de dados clicando em __Próximo__.

![Caminhos](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle2.png)

Escolha o drive do banco de dados e clique em __Próximo__.

![Drive Banco de Dados](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle3.png)

Entre com os dados para a configuração do Banco de Dados.

![Configuração Banco de Dados](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle4.png)

Confirme que leu e entendeu as cláusulas sobre os direitos autorais clicando em __Confirmar__.

![Direitos Autorais](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle5.png)

O Sistema fará uma checagem sobre os requerimentos mínimos e marcará de vermelho as pendências obrigatórias.

![Pendências](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle6.png)

Caso não tenha instalado o __php intl__ faça a instalação via apt-get:

`sudo apt-get install php-intl`

![Instalação php intl](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle7.png)

Depois reinicie o servidor Apache usando o comando:

`sudo systemctl restart apache2`

Se não houver mais pendências clique no botão continuar.

![Sem pendências](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle8.png)

Clique no botão __Continuar__ depois que o sistema terminar de processar.

![Checagem](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle9.png)

Será carregada uma tela para configuração do administrador principal, onde deverá ser preenchido pelo menos os campos de senha, primeiro nome, sobrenome e email.

![Cadastro Administrador Principal](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle10.png)

Por final será carregada a tela do Painel do Moodle.

![Painel Moodle](https://github.com/raoever/relatorio_ISW/blob/main/moodle/moodle10.png)
