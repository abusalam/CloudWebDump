Clone the repo:

$ git clone https://github.com/abusalam/CloudWebDump.git


Extract the WebDump

$ tar -xvf WebDump-20201126-1110.tar.xz

$ xz -dc drupal-20201126-1120.sql.xz > site-deployed/mariadb-init/drupal-20201126-1120.sql

$ sed -e 's/utf8mb4_0900_ai_ci/utf8mb4_unicode_ci/g' -i site-deployed/mariadb-init/drupal-20201126-1120.sql

$ cp site-deployed/.env.dist site-deployed/.env

$ chmod +w site-deployed/web/sites/default/settings.php

$ cp settings.php site-deployed/web/sites/default/settings.php

$ cd site-deployed


Start Docker:

$ docker-compose up -d

Check Database Restore Status:

$ docker-compose logs mariadb

The above command should show the log which should say like "InnoDB: Buffer pool(s) load completed at ..." at the end

$ docker-compose exec php drupal uli webadmin

You shall get some thing like this 

http://default/user/reset/1/1606458887/InskFEQJBlOeExOyU-JfDoLhV0ZvGN6cnhqGiBonX24/login

Replace http://default with https://drupal.docker.localhost

Now open https://drupal.docker.localhost/user/reset/1/1606458887/InskFEQJBlOeExOyU-JfDoLhV0ZvGN6cnhqGiBonX24/login

Stop Docker:

$ docker-compose down -v
