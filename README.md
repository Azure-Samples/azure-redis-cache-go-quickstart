# Quickstart: Use Azure Cache for Redis with Go

In this quickstart, you will learn how to build a REST API in Go that will store and retrieve user information backed by a [HASH](https://redis.io/topics/data-types-intro#redis-hashes) data structure in [Azure Cache for Redis](../cache-overview.md). 


## Prerequisites

- Azure subscription - [create one for free](https://azure.microsoft.com/free/)
- [Go](https://golang.org/doc/install) (preferably version 1.13 or above)
- [Git](https://git-scm.com/downloads)
- An HTTP client such [curl](https://curl.se/)

## Clone the sample application

Start by cloning the application from GitHub.

1. Open a command prompt and create a new folder named `git-samples`.

    ```bash
    md "C:\git-samples"
    ```

2. Open a git terminal window, such as git bash. Use the `cd` command to change into the new folder and install the sample app.

    ```bash
    cd "C:\git-samples"
    ```

3. Run the following command to clone the sample repository. This command creates a copy of the sample app on your computer.

    ```bash
    git clone https://github.com/Azure-Samples/azure-redis-cache-go-quickstart.git
    ```

## Run the application

The application accepts connectivity and credentials in the form the environment variables. 

1. Fetch the **Host name** and **Access Keys** (available via Access Keys) for Azure Cache for Redis instance in the [Azure portal](https://portal.azure.com/)

Set them to the respective environment variables

```shell
set REDIS_HOST=<Host name e.g. <name of cache>.redis.cache.windows.net>
set REDIS_PASSWORD=<Primary Access Key>
```

In the terminal window, change to the correct folder. For example:

```shell
cd "C:\git-samples\azure-redis-cache-go-quickstart"
```

2. In the terminal, run the following command to start the application.

```shell
go run main.go
```

The HTTP server will start on port `8080`.

### Test the application

Create a few user entries. The below example uses curl client:

```bash
curl -i -X POST -d '{"id":"1","name":"foo1", "email":"foo1@baz.com"}' localhost:8080/users/
curl -i -X POST -d '{"id":"2","name":"foo2", "email":"foo2@baz.com"}' localhost:8080/users/
curl -i -X POST -d '{"id":"3","name":"foo3", "email":"foo3@baz.com"}' localhost:8080/users/
```

Fetch an existing user with its `id`:

```bash
curl -i localhost:8080/users/1
```

you should get JSON response as such

```json
{
    "email": "foo1@bar",
    "id": "1",
    "name": "foo1"
}
```

If you try to fetch a user that does not exist, you will get an HTTP `404`. For example:

```bash
curl -i localhost:8080/users/100

#response
HTTP/1.1 404 Not Found
Date: Fri, 08 Jan 2021 13:43:39 GMT
Content-Length: 0
```

## Resources

- [Azure Cache for Redis](https://docs.microsoft.com/en-us/azure/azure-cache-for-redis/cache-overview) overview
- 
