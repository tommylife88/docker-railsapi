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
+  host: <%= ENV.fetch('MYSQL_CONTAINER_HOSTNAME') { 'db' } %>
 
 development:
   <<: *default
-  database: myapi_development
+  database: <%= ENV.fetch('MYSQL_DATABASE') { 'app_development' } %>

 # Warning: The database defined as "test" will be erased and
 # re-generated from your development database when you run "rake".
 # Do not set this db to the same as development or production.
-test:
-  <<: *default
-  database: myapi_test
+#test:
+#  <<: *default
+#  database: myapi_test
 
 # As with config/credentials.yml, you never want to store sensitive information,
 # like your database password, in your source code. If your source code is
@@ -48,8 +48,8 @@ test:
 # Read https://guides.rubyonrails.org/configuring.html#configuring-a-database
 # for a full overview on how database connection configuration can be specified.
 #
-production:
-  <<: *default
-  database: myapi_production
-  username: myapi
-  password: <%= ENV['MYAPI_DATABASE_PASSWORD'] %>
+#production:
+#  <<: *default
+#  database: myapi_production
+#  username: myapi
+#  password: <%= ENV['MYAPI_DATABASE_PASSWORD'] %>
```

```bash
docker-compose up --build
```

Rails:  
http://localhost:13000

phpMyaAmin:  
http://localhost:10081

## Sample

```bash
docker-compose stop
docker-compose run --rm api bundle exec rails db:create
docker-compose run --rm api bundle exec rails g scaffold user name:string age:integer
docker-compose run --rm api bundle exec rails db:migrate
```