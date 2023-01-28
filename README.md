Переконався, що ви перебуваю в режимі swarm за допомогою ініціалізації docker swarm

Створив секрети:
echo "wordpress" | docker secret create db_password -
echo "wordpress" | docker secret create db_mysql_user -
echo "somewordpress" | docker secret create db_root_password -



Перевiрив створеннi секрети командою docker secret ls
docker secret ls
ID                          NAME               DRIVER    CREATED         UPDATED
udjvc7jdsfnemjbze25myrjnt   db_mysql_user                3 minutes ago   3 minutes ago
ppbwejvqxmit67yvt2aazjbw0   db_password                  4 minutes ago   4 minutes ago
imfqkgjjpoq7nrcvf4uscvet1   db_root_password             3 minutes ago   3 minutes ago


Виправив compose file, docker-compose.yml його я прикрiпив.

Розгорнув стек за допомогою docker stack deploy -c docker-compose.yml wordpress

Перевiрка docker stack services wordpress
ID             NAME                  MODE         REPLICAS   IMAGE               PORTS
jzl3cv9j4lag   wordpress_db          replicated   1/1        amd64/mysql:8       
4acxtpr3atqr   wordpress_wordpress   replicated   1/1        amd64/wordpress:6   *:8000->80/tcp

docker ps
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS          PORTS                 NAMES
067169d49592   amd64/mysql:8       "docker-entrypoint.s…"   24 seconds ago   Up 23 seconds   3306/tcp, 33060/tcp   wordpress_db.1.xhe8rkyvrdecsz7tnceqr8ml5
3da7de974b81   amd64/wordpress:6   "docker-entrypoint.s…"   26 seconds ago   Up 25 seconds   80/tcp                wordpress_wordpress.1.u9rvtivcznndwc2loobm4oy8t
