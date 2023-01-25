Переконався, що ви перебуваю в режимі swarm за допомогою ініціалізації docker swarm

Створив секретний файл із обліковими даними, наприклад secrets.txt:

echo "MYSQL_ROOT_PASSWORD=somewordpress" > secrets.txt
echo "MYSQL_DATABASE=wordpress" >> secrets.txt
echo "MYSQL_USER=wordpress" >> secrets.txt
echo "MYSQL_PASSWORD=wordpress" >> secrets.txt

Створив секрети:
echo "somewordpress" | docker secret create mysql_root_password -
echo "wordpress" | docker secret create mysql_database -
echo "wordpress" | docker secret create mysql_user -
echo "wordpress" | docker secret create mysql_password -


Перевiрив створеннi секрети командою docker secret ls
ID                          NAME                  DRIVER    CREATED         UPDATED
fjcuotcehh3bpub68ercz0l8f   mysql_database                  9 minutes ago   9 minutes ago
din6bly9pjva9crxa7wnv8d95   mysql_password                  9 minutes ago   9 minutes ago
bu8ag6ho3e664oevb030hgyqc   mysql_root_password             9 minutes ago   9 minutes ago
5h4muumm78nody9sdj95mwvtl   mysql_user                      9 minutes ago   9 minutes ago

Виправив compose file, docker-compose.yml його я прикрiпив.

Розгорнув стек за допомогою docker stack deploy -c docker-compose.yml wordpress

Перевiрка docker stack services wordpress
ID             NAME                  MODE         REPLICAS   IMAGE         PORTS
7j6qdfq862cg   wordpress_db          replicated   0/1        mysql:8       
6cosslmvm77v   wordpress_wordpress   replicated   1/1        wordpress:6   *:8000->80/tcp
