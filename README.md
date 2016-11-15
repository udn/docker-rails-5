# docker-rails-5
Docker file and base image for rails 5 development. https://hub.docker.com/r/udnpico/docker-rails-5/.

# Usage

Create `Dockerfile` on your Rails application root folder.
```
FROM:udnpico/docker-rails-5:0.0.1
ADD . /rails-app
EXPOSE 3000
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0", "-d"]
```

Create `docker-compose.yml` on your Rails application root folder.
```
version: '2'
services:
  app:
    image: "<your-image-name>:<your-image-tag>"
    build: .
    command: bin/rails server --port 3000 --binding 0.0.0.0
    ports:
      - "3000:3000"
    volumes:
      - .:/rails-app
```

# Execute

Execute to build your own image `docker-compose build`

# Running
Run your image with this command `docker-compose up`

# How to Contribute this project
- Fork this project
- Please create Pull Request
- Further information udnpico<at>gmail.com
