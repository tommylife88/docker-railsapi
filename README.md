# Rails(API) + MySQL on docker

## Setup

```bash
docker-compose build
docker-compose run --rm api bundle exec rails new . --api -d mysql
# Input "Y"
```

api/src/config/database.yml
```diff
   adapter: mysql2
   encoding: utf8mb4
   pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
-  username: root
-  password:
-  host: localhost
+  username: <%= ENV.fetch('MYSQL_USER') { 'root' } %>
+  password: <%= ENV.fetch('MYSQL_PASSWORD') { 'password' } %>
+  host: <%= ENV.fetch('DB_HOSTNAME') { 'db' } %>
 
 development:
   <<: *default
-  database: myapi_development
+  database: <%= ENV.fetch('MYSQL_DATABASE') { 'app_development' } %>
```

```bash
docker-compose build
docker-compose up
```

Rails:  
http://localhost:13000

phpMyaAmin:  
http://localhost:10081
