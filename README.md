## Starting in GitPod

Execute the command:

```
$ dotnet run
```

## Reproducing the issue

1. When you run the above command you get a URL in which you can reach the started application.
2. Execute the command below the URL:

```
$ curl -X GET https://{WEBAPP_URL}/feedback
```

Response: List of Feedbacks **GOOD**

3. Execute the command below:

```
$ curl -i -H "Accept: application/json" -H "Content-type: application/json" -X POST https://{WEBAPP_URL}/feedback -d "{'sentence': 'i like', 'polarity': 0, 'correct': false }"
```

Response: Bad request **BAD**

```
HTTP/1.1 400 Bad Request
Server: nginx/1.14.1
Date: Thu, 13 Dec 2018 12:11:46 GMT
Content-Length: 0
Connection: keep-alive
X-Gitpod-Region: europe-west1
X-Gitpod-WorkspaceId: f9ff821f-ee78-4c39-b5a1-d4f8cfa9f4a6
X-Gitpod-Port: 8080
```




# Additional Info for creating the container
## Building the Docker Container

```
$ docker build -t $DOCKER_USER_ID/sentiment-analysis-feedback .
```

## Creating the database

If you want to make changes to the model, you need to create a new migration and re-start the application.
To create a new migration execute:

```
$ dotnet ef migrations add $MIGRATION_NAME
```

## Building the Docker Container

```
$ docker build -t $DOCKER_USER_ID/sentiment-analysis-feedback .
```

## Running the Docker Container

```
$ docker run -it -p 5000:80 --name feedback \
    -v ${PWD}/Database:/usr/database \
    -e DATABASE_DIR=/usr/database \
       $DOCKER_USER_ID/sentiment-analysis-feedback
```

Hint: In `cmd` replace ${PWD} with %cd% -> both of these represent the current directory.