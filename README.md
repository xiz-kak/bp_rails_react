# Boilerplate for Rails & React with Docker Compose

## Reference

https://qiita.com/dl10yr/items/b76969da1c2c33595a4a

## Steps

### Edit versions

- api/Dockerfile -> ruby version
- api/Gemfile -> rails version
- front/Dockerfile -> node version

### Run commands

```
$ docker-compose run api rails new . --force --no-deps --database=postgresql --api
$ docker-compose build
$ docker-compose run --rm front sh -c "npm install -g create-react-app && create-react-app react-sample"
$ mv front/react-sample/* front/react-sample/.[^\.]* front/
$ rm -r front/react-sample
```

### Update config/database.yml

```
default: &default
  adapter: postgresql
  encoding: unicode
+ host: db
+ username: postgres
+ password: postgres
  # For details on connection pooling, see Rails configuration guide
  # https://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
```

### Run commands again

```
$ docker-compose run api rake db:create
$ docker-compose up
```

### Access

#### Rails

http://localhost:3000

#### React

http://localhost:8000
