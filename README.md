# Un tableau de bord sur la Covid
### Dashboard covid en utilisant docker (MySQL et Grafana)

Nous allons utiliser Docker pour créer des containers et les lier. Nous utiliserons 2 images pour initialiser les containers :
- mysql (base de données)
- grafana/grafana (affichage de graphe)

```version: "3.8"

services:
  db:
    image : mysql
    container_name: db
    restart : always
    environment:
      - MYSQL_ROOT_PASSWORD=root
      # - MYSQL_USER=user
      # - MYSQL_PASSWORD=user123
    ports :
      - 3306:3306
    volumes :
      - database:/var/lib/mysql
      - ./datas/vaccination.sql:/docker-entrypoint-initdb.d/vaccination.sql
    networks:
      - mysql_network
    
  grafana :
    image : grafana/grafana
    container_name: grafana
    ports :
      - 3000:3000
    networks:
      - mysql_network

volumes:
  database:
    name: database

networks:
  mysql_network:
    name: mysql_network
    ```
