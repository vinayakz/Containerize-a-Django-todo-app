# Containerize a Django todo app

**Dear Friend,**

**Building and packaging is a most frequent activity in software development.**

**Docker makes it easier to create, deploy, and run applications by using containers.**

**Building and running docker container is a three step process as illustrated here.**

**Read on further for detailed steps :)**

![Docker](https://media.licdn.com/dms/image/D4E12AQFOkyFj98EtRw/article-inline_image-shrink_1500_2232/0/1672090115942?e=1677715200&v=beta&t=961jIqpyVUI_QvIYiFAiiHaI5gYDUuo0p_5aUeZ_Ll8)


## How to containerise an app?

**Step 1 : Write Dockerfile and place inside your project**

- **create vi Dockerfile**

- **The Dockerfile is a set of instructions that specify how to build a Docker image.**

- **When you run the docker build command, Docker reads the Dockerfile to build the image.**


```sh
  FROM python:3
  RUN pip install django==3.2

  COPY . .

  RUN python manage.py migrate
  EXPOSE 8000
  CMD ["python","manage.py","runserver","0.0.0.0:8000"]
```

**In this Dockerfile:**

1. The FROM instruction specifies the base image. In this case, the base image is python:3. This is a version of python which is built on top of the lightweight python distribution.

2. The COPY instruction copies files from the host filesystem into the image. In this case, it is copying the entire current directory (.) into the (.) directory in the image.

3. The RUN instruction runs a n this case, This will create all the migrations file (database migrations) required to run this App.

4. Writing EXPOSE in your Dockerfile, is merely a hint that a certain port is useful. Docker won’t do anything with that information by itself.

5. The CMD instruction specifies the default command to execute when a container is started from the image.

**Step 2 : Build a Docker Image**

1. The docker build command will build a Docker image from a Dockerfile.

2. The -t option specifies the name. The . at the end of the command indicates the build context, which is the location of the Dockerfile.

3. In this case, the docker build command will build an image from the Dockerfile in the current directory (indicated by the .) and give it the name todo-app.

 ```sh
 
 RUN sudo docker build . -t todo app
 
 ```
 
4. After the above step, you an find a Docker Image named todo-app in your docker.

**Step 3: Run the application using the container image**

```sh

sudo docker run  -p 8001:8001  todo-app

```

### The docker run command would to start a new container from an image.

1. The -p 8000:8000 option maps the container's port 8000 to the host's port 8000. This means that traffic sent to the host's port 8000 will be forwarded to the container's port 8000.

2. The todo-app at the end of the command is the name of the image that the container will be created from.

3. The docker run command starts a new container from the todo-app image. And forward traffic from the host's port 8000 to the container's port 8000.

4. This is useful when the todo-app image contains a web server that listens on port 8000. It allows you to access the service running in the container by connecting to the host's port 8000.

5. In this example you could access the app by opening a web browser and navigating to http://localhost:8000.

## Next steps

## You can get the sample app to get started on building and running a container.

**PROJECT :- https://github.com/vinayakz/django-todo-cicd**
