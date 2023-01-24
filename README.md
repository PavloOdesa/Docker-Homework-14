Переконався, що ви перебуваю в режимі swarm за допомогою ініціалізації docker swarm

Створив секретний файл із обліковими даними, наприклад secrets.txt:

echo "MYSQL_ROOT_PASSWORD=somewordpress" > secrets.txt
echo "MYSQL_DATABASE=wordpress" >> secrets.txt
echo "MYSQL_USER=wordpress" >> secrets.txt
echo "MYSQL_PASSWORD=wordpress" >> secrets.txt

Створіть секрети за допомогою команди docker secret create:

docker secret create mysql_root_password secrets.txt
docker secret create mysql_database secrets.txt
docker secret create mysql_user secrets.txt
docker secret create mysql_password secrets.txt

Перевiрив створеннi секрети командою docker secret ls
ID                          NAME                  DRIVER    CREATED          UPDATED
va8p0bcmlfipbuzoojrihkay4   mysql_database                  24 minutes ago   24 minutes ago
ytymsdteswdv6xktsi67va3ly   mysql_password                  24 minutes ago   24 minutes ago
ivw8ioep5lt7oy9wespu1ghj1   mysql_root_password             24 minutes ago   24 minutes ago
ks4icm9goo8ccgj6uh5pln3ar   mysql_user                      24 minutes ago   24 minutes ago

Виправив compose file, docker-compose.yml його я прикрiпив.

Розгорнув стек за допомогою docker stack deploy -c docker-compose.yml wordpress

Перевiрка docker stack services wordpress
ID             NAME                  MODE         REPLICAS   IMAGE         PORTS
7j6risq753cg   wordpress_db          replicated   0/1        mysql:8       
6cyyslmvm66v   wordpress_wordpress   replicated   1/1        wordpress:6   *:8000->80/tcp
