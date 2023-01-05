## Engineeer Guide for better Productivity


### Docker Command Sets
1.  `docker run`: This command is used to run a Docker container. For example: `docker run ubuntu:20.04` This command will run an Ubuntu 20.04 container.
    
2.  `docker start`: This command is used to start a stopped Docker container. For example: `docker start my_container` This command will start the container with the name "my_container".
    
3.  `docker stop`: This command is used to stop a running Docker container. For example: `docker stop my_container` This command will stop the container with the name "my_container".
    
4.  `docker build`: This command is used to build a Docker image from a Dockerfile. For example: `docker build -t my_image .` This command will build an image named "my_image" from the Dockerfile in the current directory.
    
5.  `docker push`: This command is used to push a Docker image to a registry, such as Docker Hub. For example: `docker push my_image` This command will push the image "my_image" to Docker Hub.
    
6.  `docker pull`: This command is used to pull a Docker image from a registry, such as Docker Hub. For example: `docker pull ubuntu:20.04` This command will pull the Ubuntu 20.04 image from Docker Hub.
7.  `docker network create`: This command is used to create a new Docker network. For example: `docker network create my_network` This command will create a new network named "my_network".
8.  `docker network ls`: This command is used to list all the networks on the Docker host.
9.  `docker network inspect`: This command is used to view detailed information about a Docker network. For example: `docker network inspect my_network`
10. Run a mysql container inside docker: `docker run --name my_mysql --network my_network -e MYSQL_ROOT_PASSWORD=password -d mysql:8.0`

**Building, deploying a NodeJS app on Docker**
To build a Docker image for an Express Node.js app and run the Docker container, you will need to create a `Dockerfile` and use the `docker build` and `docker run` commands.

Here is an example `Dockerfile` that can be used to build a Docker image for an Express Node.js app:

Copy code
```dockerfile
# Use the latest LTS version of Node.js as the base image
FROM node:lts
# Set the working directory
WORKDIR /app
# Copy the package.json and package-lock.json files to the working directory
COPY package*.json ./
# Install the dependencies
RUN npm install
# Copy the rest of the app's source code to the working directory
COPY . .
# Expose the app's port
EXPOSE 3000

# Start the app
CMD ["npm", "start"]
```
This `Dockerfile` will use the latest LTS version of Node.js as the base image, set the working directory to `/app`, copy the `package.json` and `package-lock.json` files to the working directory, install the app's dependencies, copy the rest of the app's source code to the working directory, expose the app's port, and start the app when the container is run.

To build the Docker image, run the following command from the directory containing the `Dockerfile`:

`docker build -t my-app .` 

This will build a Docker image for the app and give it the tag `my-app`.

To run the Docker container, use the following command:

`docker run -p 3000:3000 my-app` 

This will run the Docker container and map the container's port 3000 to the host's port 3000, allowing you to access the app on `http://localhost:3000`.

**Running .net core app in Docker**
To build a Docker image for a .NET Core API application and run the Docker container, you will need to create a `Dockerfile` and use the `docker build` and `docker run` commands.

Here is an example `Dockerfile` that can be used to build a Docker image for a .NET Core API application:

Copy code
```dockerfile
# Use the latest .NET Core SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:latest

# Set the working directory
WORKDIR /app

# Copy the project file to the working directory
COPY *.csproj ./

# Restore the dependencies
RUN dotnet restore

# Copy the rest of the source code to the working directory
COPY . .

# Build the app
RUN dotnet build

# Expose the app's port
EXPOSE 80

# Start the app
CMD ["dotnet", "run", "--urls", "http://*:80"]
```

This `Dockerfile` will use the latest .NET Core SDK image as the base image, set the working directory to `/app`, copy the project file to the working directory, restore the dependencies, copy the rest of the source code to the working directory, build the app, expose the app's port, and start the app when the container is run.

To build the Docker image, run the following command from the directory containing the `Dockerfile`:

`docker build -t my-app .` 

This will build a Docker image for the app and give it the tag `my-app`.

To run the Docker container, use the following command:

`docker run -p 80:80 my-app` 

This will run the Docker container and map the container's port 80 to the host's port 80, allowing you to access the app on `http://localhost`.

Alternatively, you can use the `-d` option to run the container in detached mode, which allows the container to run in the background:

`docker run -d -p 80:80 my-app` 

This will run the Docker container in detached mode and map the container's port 80 to the host's port 80. You can use the `docker ps` command to list the running containers, and the `docker stop` command to stop a running container.

### Using WSL 2
1.  Make sure you are running Windows 10 version 2004 or higher.
2.  Enable the "Windows Subsystem for Linux" feature. You can do this by going to "Control Panel" > "Programs" > "Turn Windows features on or off" and checking the "Windows Subsystem for Linux" option.
3.  Restart your computer when prompted.
4.  Download and install a Linux distribution from the Microsoft Store.
5.  Launch the Linux distribution and complete the setup process.

Once you have WSL 2 set up, you can use it with Visual Studio Code by following these steps:

1.  Install the Remote Development extension pack for Visual Studio Code.
2.  Open the Command Palette (Ctrl+Shift+P) and select the "Remote-WSL: New Window" command. This will open a new Visual Studio Code window that is connected to WSL.
3.  You can then use this window to work with files and directories in WSL, as well as run command-line tools and develop applications as if you were working directly on the Linux command line.

### NO SQL and MONGO
1.  **Querying data**:

To query data from a collection, you can use the `find()` method. For example, to query all documents in the "users" collection:
`db.users.find()`
You can also specify a filter to return only certain documents. For example, to query all documents in the "users" collection where the "age" field is greater than 30:
`db.users.find({ age: { $gt: 30 } })`
2.  **Searching data**:
To search for text within documents in a collection, you can use the `$text` operator. For example, to search for documents in the "articles" collection that contain the word "MongoDB":
`db.articles.find({ $text: { $search: "MongoDB" } })`
3.  **Aggregation**:
To perform aggregation operations in MongoDB, you can use the `aggregate()` method. For example, to find the total number of documents in the "orders" collection:
`db.orders.aggregate([{ $count: "total" }])`
You can also use pipeline stages in the `aggregate()` method to perform more complex aggregation operations, such as group by and match.
4.  **Joining collections**:
To perform a "join" operation in MongoDB, you can use the `$lookup` operator in the `aggregate()` method. For example, to "join" the "orders" and "products" collections to find the product details for each order:
`db.orders.aggregate([
   {
      $lookup:
         {
           from: "products",
           localField: "productId",
           foreignField: "_id",
           as: "product_details"
         }
   }
])`
This will add a new field called "product_details" to each document in the "orders" collection, which contains the details of the product associated with the order.
5.  **Other common actions**:
Here are some other common actions you might need to perform in MongoDB:

-   To insert a new document into a collection, use the `insertOne()` or `insertMany()` method.
-   To update a document, use the `updateOne()` or `updateMany()` method.
-   To delete a document, use the `deleteOne()` or `deleteMany()` method.
6. **Pipelining**
In MongoDB, pipelining refers to the process of passing the output of one operation as the input to another operation, allowing you to chain multiple operations together in a single query. This can be useful for performing complex data processing tasks, such as aggregations and transformations.

For example, you might use pipelining to group documents by a certain field, perform calculations on those groups, and then sort the results. You can use various pipeline stages, such as `$group`, `$sort`, `$match`, and `$project`, to specify the different operations you want to perform.
`Suppose we have a collection of student records, with each document containing fields for the student's name, age, and grades in different subjects. We want to find the top 10 students with the highest average grade.
Suppose we have a collection of student records, with each document containing fields for the student's name, age, and grades in different subjects. We want to find the top  10 students with the highest average grade.

`
db.students.aggregate([
   {
      $group: {
         _id: "$name",
         average: { $avg: "$grades.math" }
      }
   },
   {
      $sort: { average: -1 }
   },
   {
      $limit: 10
   }
])
`
This query uses the following pipeline stages:

1.  `$group`: This stage groups the documents by the "name" field and calculates the average grade in the "math" subject for each student.
2.  `$sort`: This stage sorts the documents by the "average" field in descending order.
3.  `$limit`: This stage limits the number of documents returned to the top 10 students with the highest average grade.

The output of this query will be a list of the top 10 students, ranked by average grade in the "math" subject.

### GIT Basics
#### Setting up GIT
1.  Install Git on your local machine. You can download the latest version of Git from the official website at [https://git-scm.com/](https://git-scm.com/).
    
2.  Set up your Git user name and email address. This is important because Git tracks changes by user, and you'll want to be able to identify your changes in the Git history. To set your user name and email address, use the following commands:
`git config --global user.name "Your Name"
git config --global user.email "your@email.com"` 

3.  To use an existing Git repository, you'll need to clone it to your local machine. To do this, use the `git clone` command followed by the URL of the repository. For example:

`git clone https://github.com/my-username/my-repo.git` 

This command will clone the repository at the URL "[https://github.com/my-username/my-repo.git](https://github.com/my-username/my-repo.git)" to a local directory called "my-repo".

4.  To create a new Git repository, use the `git init` command followed by the name of the directory you want to create the repository in. For example:

`git init my-repo` 

This command will create a new Git repository in a directory called "my-repo".

#### Using GIT
1.  `git clone`: This command is used to clone a Git repository from a remote server to your local machine. For example: `git clone https://github.com/my-username/my-repo.git` This command will clone the repository at the URL "[https://github.com/my-username/my-repo.git](https://github.com/my-username/my-repo.git)" to a local directory called "my-repo".
    
2.  `git status`: This command is used to view the status of the files in the current Git repository. It will show you which files have been modified, added, or deleted since the last commit.
    
3.  `git add`: This command is used to stage changes for the next commit. For example: `git add my-file.txt` This command will stage the changes to the file "my-file.txt" for the next commit.
    
4.  `git commit`: This command is used to save your staged changes to the Git repository. For example: `git commit -m "Add new feature"` This command will commit the staged changes with the commit message "Add new feature".
    
5.  `git push`: This command is used to push your

6.  `git stash`:

Git stash is a command that allows you to save changes that you have made to your working copy, but are not ready to commit, in a temporary stash. This can be useful if you need to switch branches or switch to a different task, but don't want to commit your changes yet.

To use `git stash`, use the `git stash save` command followed by a message describing your changes. For example:

`git stash save "WIP: Adding new feature"` 

This will save your changes to the stash and revert your working copy to the state it was in before you made the changes.

To apply the changes from the stash to your working copy, use the `git stash pop` command. For example:

`git stash pop`

#### Merging remote code using Git
To merge remote code into your local repository, you'll need to first fetch the remote code and then merge it into your local branch.

To fetch the remote code, use the `git fetch` command followed by the name of the remote repository. For example:

`git fetch origin` 

This will fetch the code from the "origin" remote repository and update your local copy of the repository.
To merge the remote code into your local branch, use the `git merge` command followed by the name of the remote branch. For example:

`git merge origin/my-branch` 

This will merge the code from the "my-branch" branch in the "origin" remote repository into your local "my-branch" branch.

### REST 
REST (Representational State Transfer) is a software architectural style that defines a set of constraints and properties for building web services. REST APIs use HTTP methods to send and receive data, and are typically used to create, read, update, and delete (CRUD) data in web applications.

Here are the most common HTTP methods used in REST APIs, along with examples of how they are used:

1.  `GET`: Used to retrieve data from the server. For example:

`curl -X GET \
  https://api.example.com/users/123 \
  -H 'Accept: application/json'` 

This `curl` command sends an HTTP GET request to the "[https://api.example.com/users/123](https://api.example.com/users/123)" URL, which retrieves the user with ID 123 from the server.

2.  `POST`: Used to create new data on the server. For example:


`curl -X POST \
  https://api.example.com/users \
  -H 'Content-Type: application/json' \
  -d '{"name":"John","email":"john@example.com"}'` 

This `curl` command sends an HTTP POST request to the "[https://api.example.com/users](https://api.example.com/users)" URL, with a "Content-Type" header of "application/json" and a JSON request body containing the data for the new user.

Other CURL commands
1.  Posting form data:

To send form data to a REST API using `curl`, use the `-X` flag followed by the `POST` method, the `-d` flag to specify the form data, and the URL of the API endpoint as the argument. For example:

`curl -X POST \
  https://api.example.com/users \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'name=John&email=john@example.com'` 

This `curl` command sends an HTTP POST request to the "[https://api.example.com/users](https://api.example.com/users)" URL, with a "Content-Type" header of "application/x-www-form-urlencoded" and form data containing the name and email of the user.

2.  Uploading a file:

To upload a file to a REST API using `curl`, use the `-X` flag followed by the `POST` method, the `-F` flag to specify the file, and the URL of the API endpoint as the argument. For example:

`curl -X POST \
  https://api.example.com/users/123/avatar \
  -H 'Content-Type: multipart/form-data' \
  -form 'avatar=@"c:\Users\shantanu.singh\Desktop\myfile.txt"'`
  
  
  ### Session Management through Redis
  Redis is an in-memory data structure store that can be used as a database, cache, and message broker. It supports various data structures such as strings, hashes, lists, sets, and more.

Here are some basic Redis commands for managing data:

-   SET: Sets a value for a key. For example: `SET key value`
-   GET: Retrieves the value of a key. For example: `GET key`
-   EXISTS: Determines if a key exists. For example: `EXISTS key`
-   DEL: Deletes a key and its value. For example: `DEL key`
Redis works over the Redis protocol, which is a simple, text-based protocol for sending commands and receiving responses. You can use the `redis-cli` command-line utility to send commands to a Redis server and view the responses.

To use `redis-cli` to query a Redis store on Windows, follow these steps:

1.  Download and install Redis on your Windows machine. This will also install `redis-cli`.
2.  Open the Command Prompt.
3.  Type `redis-cli` and press Enter. This will launch the `redis-cli` utility and connect to the Redis server running on localhost.
4.  Type a Redis command and press Enter to send it to the server. For example, to get the value of a key, you can use the `GET` command: `GET key`
5.  The server will respond with the result of the command.

Here is an example of using `redis-cli` to set and get a key-value pair:

`C:\> redis-cli
127.0.0.1:6379> SET key value
OK
127.0.0.1:6379> GET key
"value"` 

You can also specify the host and port of the Redis server using the `-h` and `-p` options, respectively. For example:

`redis-cli -h host -p port` 

This will connect to the Redis server running on the specified host and port.

Here is an example of how to use StackExchange.Redis to perform basic Redis operations in a .NET application:

Copy code

```C#
using StackExchange.Redis;
namespace RedisExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Connect to the Redis server
            var connection = ConnectionMultiplexer.Connect("localhost");
            var database = connection.GetDatabase();

            // Set a key-value pair
            database.StringSet("key", "value");

            // Get the value of a key
            var value = database.StringGet("key");
            Console.WriteLine(value);

            // Check if a key exists
            var keyExists = database.KeyExists("key");
            Console.WriteLine(keyExists);

            // Delete a key
            database.KeyDelete("key");

            // Check if a key exists again
            keyExists = database.KeyExists("key");
            Console.WriteLine(keyExists);
        }
    }
}
```

This example demonstrates how to connect to a Redis server, set a key-value pair, get the value of a key, check if a key exists, delete a key, and check if a key exists again.

To use Redis with Node.js, you can use the `redis` library. Here is an example of how to use the `redis` library to perform basic Redis operations in a Node.js application:

```javascript
const redis = require('redis');

// Connect to the Redis server
const client = redis.createClient();

// Set a key-value pair
client.set('key', 'value', redis.print);

// Get the value of a key
client.get('key', (error, result) => {
  console.log(result);
});

// Check if a key exists
client.exists('key', (error, result) => {
  console.log(result === 1);
});

// Delete a key
client.del('key', redis.print);

// Check if a key exists again
client.exists('key', (error, result) => {
  console.log(result === 1);
});

// Disconnect from the Redis server
client.quit();
```

#### Session Management With Redis

This example demonstrates how to connect to a Redis server, set a key-value pair, get the value of a key, check if a key exists, delete a key, and check if a key exists again.

To manage user sessions in a load-balanced environment, you can use Redis to store session data using the session ID as the key. For example:

```javascript
const redis = require('redis');

// Connect to the Redis server
const client = redis.createClient();

// Store session data
client.set(`session:${sessionId}`, JSON.stringify(sessionData), redis.print);

// Retrieve session data
client.get(`session:${sessionId}`, (error, result) => {
  const sessionData = JSON.parse(result);
});
``` 

This will allow you to store and retrieve session data using Redis, regardless of which application server the user is connected to.


### Using Quality Gate for Code Quality
SonarQube is a tool that can be used to perform static code analysis and track code quality over time. It can be used with Visual Studio Code and Visual Studio for .NET projects to enable quality gates.

To use SonarQube with Visual Studio Code:

1.  Install the SonarLint extension for Visual Studio Code.
2.  Connect to a SonarQube server by going to the SonarLint view in the sidebar and clicking the "Connect to a SonarQube or SonarCloud instance" button.
3.  Select the project you want to analyze and click the "Analyze" button.
4.  SonarLint will analyze the project and display any issues it finds in the Problems view.

To use SonarQube with Visual Studio for .NET:

1.  Install the SonarQube Extension for Visual Studio.
2.  Connect to a SonarQube server by going to the Team Explorer view and clicking the "Manage Connections" button.
3.  Select the project you want to analyze and click the "Analyze" button.
4.  SonarQube will analyze the project and display any issues it finds in the Error List view.

In both cases, you can use the quality gate defined on the SonarQube server to ensure that your code meets certain quality standards before it is deployed. If the code does not meet the quality standards, the analysis will fail and the deployment will be blocked.

### Messaging Queue and RabbitMQ
A message queue is a software system that enables the exchange of messages between different application components or systems. Messages are typically sent asynchronously, meaning that the sender and receiver do not need to be running at the same time. Message queues can be used to decouple systems, improve scalability, and provide reliability.

RabbitMQ is an open-source message queue system that implements the Advanced Message Queuing Protocol (AMQP). It can be used to exchange messages between different applications and systems in a reliable and scalable way.

To use RabbitMQ with .NET, you can use the RabbitMQ .NET client library. Here is an example of how to use the RabbitMQ .NET client to send and receive messages in a .NET application:



```c#
using RabbitMQ.Client;
using RabbitMQ.Client.Events;

namespace RabbitMQExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Connect to the RabbitMQ server
            var factory = new ConnectionFactory() { HostName = "localhost" };
            using (var connection = factory.CreateConnection())
            using (var channel = connection.CreateModel())
            {
                // Declare a queue
                channel.QueueDeclare(queue: "hello", durable: false, exclusive: false, autoDelete: false, arguments: null);

                // Send a message
                string message = "Hello World!";
                var body = Encoding.UTF8.GetBytes(message);
                channel.BasicPublish(exchange: "", routingKey: "hello", basicProperties: null, body: body);
                Console.WriteLine(" [x] Sent {0}", message);

                // Receive a message
                var consumer = new EventingBasicConsumer(channel);
                consumer.Received += (model, ea) =>
                {
                    var body = ea.Body;
                    var message = Encoding.UTF8.GetString(body);
                    Console.WriteLine(" [x] Received {0}", message);
                };
                channel.BasicConsume(queue: "hello", autoAck: true, consumer: consumer);

                Console.WriteLine(" Press [enter] to exit.");
                Console.ReadLine();
            }
        }
    }
}
```

This example demonstrates how to connect to a RabbitMQ server, declare a queue, send a message, and receive a message.

To use RabbitMQ with Node.js, you can use the `amqplib` library. Here is an example of how to use `amqplib` to send and receive messages in a Node.js application:


```javascript
const amqp = require('amqplib');

// Connect to the RabbitMQ server
amqp.connect('amqp://localhost').then(connection => {
  // Create a channel
  return connection.createChannel();
}).then(channel => {
  // Declare a queue
  const queue = 'hello';
  channel.assertQueue(queue, {
    durable: false
  });

  // Send a message
  channel.sendToQueue(queue, Buffer.from('Hello World!'));
  console.log(" [x] Sent 'Hello World!'");

  // Receive a message
  channel.consume(queue, message => {
    console.log(" [x] Received %s", message.content.toString())
```

### Linux command set
Here are some common Linux (Ubuntu) commands that can make a developer more productive:

1.  `grep`: Search for a pattern in a file or output. For example: `grep "ERROR" log.txt` will search for the string "ERROR" in the file `log.txt`.
2.  `find`: Search for files or directories matching a pattern. For example: `find . -name "*.txt"` will search for all files with a `.txt` extension in the current directory and its subdirectories.
3.  `awk`: Process text data by specifying a pattern to search for. For example: `awk '/ERROR/ {print $0}' log.txt` will print all lines in `log.txt` that contain the string "ERROR".
4.  `sed`: Modify text data by specifying a pattern to search for. For example: `sed 's/ERROR/INFO/g' log.txt` will replace all occurrences of "ERROR" with "INFO" in `log.txt`.
5.  `xargs`: Execute a command with arguments taken from standard input. For example: `find . -name "*.txt" | xargs grep "ERROR"` will search for all files with a `.txt` extension in the current directory and its subdirectories, and search for the string "ERROR" in each file.

#### Listening Port

**Linux**

To get the listening port and process in Linux, you can use the `lsof` command.

For example, to get the listening port and process for all network connections, you can use the following command:

```bash
lsof -i -P -n` 
COMMAND  PID     USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
node      22 shantanu   18u  IPv4     35      0t0  TCP 127.0.0.1:45199 (LISTEN)
node      22 shantanu   21u  IPv4  23562      0t0  TCP 127.0.0.1:45199->127.0.0.1:47900 (ESTABLISHED)
node     114 shantanu   18u  IPv4  22587      0t0  TCP 127.0.0.1:47900->127.0.0.1:45199 (ESTABLISHED)
node     123 shantanu   18u  IPv4  18683      0t0  TCP 127.0.0.1:47906->127.0.0.1:45199 (ESTABLISHED)
node     161 shantanu   19u  IPv4  23564      0t0  TCP 127.0.0.1:45199->127.0.0.1:47906 (ESTABLISHED)
node     161 shantanu   43u  IPv4    751      0t0  TCP 127.0.0.1:53673 (LISTEN)
node     161 shantanu   47u  IPv4    752      0t0  TCP 127.0.0.1:39234->127.0.0.1:53673 (ESTABLISHED)
node     161 shantanu   49u  IPv4    753      0t0  TCP 127.0.0.1:53673->127.0.0.1:39234 (ESTABLISHED)
node     161 shantanu   55u  IPv4    786      0t0  TCP 127.0.0.1:53543 (LISTEN)
node     161 shantanu   57u  IPv4    787      0t0  TCP 127.0.0.1:44944->127.0.0.1:53543 (ESTABLISHED)
node     161 shantanu   58u  IPv4    788      0t0  TCP 127.0.0.1:53543->127.0.0.1:44944 (ESTABLISHED)
node    1742 shantanu   25u  IPv4  25821      0t0  TCP 127.0.0.1:53777 (LISTEN)
```
This will list all network connections and their corresponding process ID, protocol, and port.

You can also use the `-t` option to only show the process ID, and the `-s` option to specify the protocol. For example, to get the listening port and process for all TCP connections, you can use the following command:


`lsof -i -P -n -s TCP -t` 

This will list all TCP connections and their corresponding process ID.

You can also use the `-i` option to filter the connections by protocol and port. For example, to get the listening port and process for all connections on port 80, you can use the following command:


`lsof -i -P -n -s TCP -t :80` 

This will list all connections on port 80 and their corresponding process ID.

**Windows**
o get the listening port and process in Windows using PowerShell, you can use the `Get-NetTCPConnection` cmdlet.

For example, to get the listening port and process for all TCP connections, you can use the following command:


`Get-NetTCPConnection | Select-Object -Property LocalAddress, LocalPort, OwningProcess` 

This will list all TCP connections and their corresponding local address, local port, and owning process.

You can also use the `-State` parameter to filter the connections by state. For example, to get the listening port and process for all established TCP connections, you can use the following command:


```powershell
PS C:\Users\shantanu.singh> Get-NetTCPConnection -State Listen | Select-Object -Property LocalAddress, LocalPort, OwningProcess

LocalAddress  LocalPort OwningProcess
------------  --------- -------------
::                49678          4092
::                49676          1032
::1               49671          5504
::                49670          1068
::                49668          5036
::                49667          3532
::                49666          2072

```

This will list all established TCP connections and their corresponding local address, local port, and owning process.

You can also use the `Get-Process` cmdlet to get more information about the processes. For example, to get the process name and command line arguments for a process with a given process ID, you can use the following command:


`Get-Process -Id <process ID> | Select-Object -Property Name, CommandLine` 

This will print the process name and command line arguments for the specified process ID.

You can also use the `Where-Object` cmdlet to filter the connections by port. For example, to get the listening port and process for all connections on port 80, you can use the following command:

`Get-NetTCPConnection | Where-Object {$_.LocalPort -eq 80} | Select-Object -Property LocalAddress, LocalPort, OwningProcess` 

This will list all connections on port 80 and their corresponding local address, local port, and owning process.

#### Searching Premier

**Searching in linux**
To recursively search for a string in files using `grep`, you can use the `-r` or `--recursive` option. This will search for the string in all files in the specified directory and its subdirectories.

For example, to search for the string "ERROR" in all files in the `/var/log` directory and its subdirectories, you can use the following command:


`grep -r "ERROR" /var/log` 

This will search for the string "ERROR" in all files in the `/var/log` directory and its subdirectories, and print the results to the console.

You can also use the `-n` or `--line-number` option to print the line numbers of the matching lines. For example:


`grep -rn "ERROR" /var/log` 

This will print the line numbers of the matching lines in addition to the matching lines themselves.

You can use the `-i` or `--ignore-case` option to perform a case-insensitive search. For example:


`grep -rin "error" /var/log` 

This will search for the string "error" (regardless of case) in all files in the `/var/log` directory and its subdirectories, and print the results to the console.

**To search for the string "needle" in all files whose name ends with `.js` in the `/myproj/v1` directory, ignoring case, you can use the following command:**

`grep -rin "needle" /myproj/v1 --include "*.js"` 


You can use the `--exclude` option to exclude certain files or directories from the search. For example:


`grep -rin "needle" /myproj/v1 --include "*.js" --exclude "node_modules"` 

This will search for the string "needle" (regardless of case) in all files in the `/myproj/v1` directory whose name ends with `.js`, but will exclude the `node_modules` directory and its subdirectories from the search.

You can use the `-l` or `--files-with-matches` option to print only the names of the files that contain a match, rather than the matching lines themselves. For example:

`grep -ril "needle" /myproj/v1 --include "*.js"` 

This will search for the string "needle" (regardless of case) in all files in the `/myproj/v1` directory whose name ends with `.js`, and print only the names of the files that contain a match.

**Searching file**
To recursively search for a file in Linux, you can use the `find` command.

For example, to search for a file named `example.txt` in the current directory and its subdirectories, you can use the following command:

Copy code

`find . -name "example.txt"` 

This will search for a file named `example.txt` in the current directory and its subdirectories, and print the path to the file if it is found.

You can also use the `-type` option to search for specific types of files. For example, to search for a directory named `mydir` in the current directory and its subdirectories, you can use the following command:


`find . -type d -name "mydir"` 

This will search for a directory named `mydir` in the current directory and its subdirectories, and print the path to the directory if it is found.

You can also use the `-exec` option to execute a command on the found files. For example, to search for a file named `example.txt` in the current directory and its subdirectories, and print the contents of the file if it is found, you can use the following command:


`find . -name "example.txt" -exec cat {} \;`

To recursively search for a file in a specific directory and its subdirectories in Linux, you can use the `find` command and specify the directory as the starting point for the search.

For example, to search for a file named `example.txt` in the `/var/log` directory and its subdirectories, you can use the following command:

`find /var/log -name "example.txt"`

#### Searching in Windows
To search for the string "needle" in all files whose name ends with `.js` in the `C:\myproj\v1` directory, ignoring case, using PowerShell, you can use the following command:


`Get-ChildItem -Path "C:\myproj\v1" -Include "*.js" -Recurse | Select-String -Pattern "needle" -CaseSensitive:$false` 

This will search for the string "needle" (regardless of case) in all files in the `C:\myproj\v1` directory whose name ends with `.js`, and print the results to the console.

You can use the `-Exclude` parameter to exclude certain files or directories from the search. For example:


`Get-ChildItem -Path "C:\myproj\v1" -Include "*.js" -Exclude "node_modules" -Recurse | Select-String -Pattern "needle" -CaseSensitive:$false` 

This will search for the string "needle" (regardless of case) in all files in the `C:\myproj\v1` directory whose name ends with `.js`, but will exclude the `node_modules` directory and its subdirectories from the search.

You can use the `-List` parameter to print only the names of the files that contain a match, rather than the matching lines themselves. For example:


`Get-ChildItem -Path "C:\myproj\v1" -Include "*.js" -Recurse | Select-String -Pattern "needle" -CaseSensitive:$false -List` 

This will search for the string "needle" (regardless of case) in all files in the `C:\myproj\v1` directory whose name ends with `.js`, and print only the names of the files that contain a match.

**Searching for file in windows**

To recursively search for a file in a specific directory and its subdirectories in Windows using PowerShell, you can use the `Get-ChildItem` cmdlet and specify the directory as the starting point for the search.

For example, to search for a file named `example.txt` in the `C:\myproj` directory and its subdirectories, you can use the following command:


`Get-ChildItem -Path "C:\myproj" -Recurse | Where-Object {$_.Name -eq "example.txt"}` 

This will search for a file named `example.txt` in the `C:\myproj` directory and its subdirectories, and print the path to the file if it is found.

You can also use the `-Directory` parameter to search for directories instead of files. For example, to search for a directory named `mydir` in the `C:\myproj` directory and its subdirectories, you can use the following command:

`Get-ChildItem -Path "C:\myproj" -Directory -Recurse | Where-Object {$_.Name -eq "mydir"}` 

This will search for a directory named `mydir` in the `C:\myproj` directory and its subdirectories, and print the path to the directory if it is found.

### Managing Process
To search for a process in the process list in Linux, you can use the `ps` or `pgrep` command.

For example, to search for a process with the name `example`, you can use the following command:

`ps -ef | grep example` 

This will list all processes with the name `example` and their corresponding process ID, user, and command line arguments.

You can also use the `pgrep` command to search for processes by name:

`pgrep example` 

This will print the process IDs of all processes with the name `example`.
For example, to search for a process with the name `example`, you can use the following command:

`Get-Process -Name example` 

This will list all processes with the name `example` and their corresponding process ID, name, and command line.


### Scheduling Tasks
#### Linux
To schedule a task in Linux, you can use the `crontab` command.

The `crontab` command allows you to schedule tasks to be run automatically at specific intervals. You can use it to schedule tasks to run daily, weekly, monthly, or at any other interval.

To schedule a task using `crontab`, you will need to create a crontab file that specifies the task to be run and the schedule for running the task.

Here is an example of how to schedule a task to run a script every day at 10:00 AM using `crontab`:

Copy code

`0 10 * * * /path/to/script.sh` 

This crontab entry will run the `script.sh` script every day at 10:00 AM.

To schedule a task in Windows, you can use the Task Scheduler.

The Task Scheduler is a built-in Windows tool that allows you to schedule tasks to be run automatically at specific intervals. You can use it to schedule tasks to run daily, weekly, monthly, or at any other interval.

#### Windows
To schedule a task using the Task Scheduler, follow these steps:

1.  Open the Task Scheduler by typing "task scheduler" into the Start menu search bar and pressing Enter.
2.  In the Task Scheduler window, click the "Create Basic Task" option in the Actions panel on the right.
3.  In the "Create Basic Task" wizard, enter a name and description for the task, and then click the "Next" button.
4.  Select the trigger for the task. For example, to run the task daily, select the "Daily" option and specify the start date and time.
5.  Select the action for the task. For example, to run a script, select the "Start a program" option and specify the path to the script.
6.  Review the task settings and click the "Finish" button to create the task.

The task will now be scheduled to run at the specified interval. You can use the Task Scheduler to view, edit, or delete the task at any time.

Here is an example of how to schedule a task to run a script every day at 10:00 AM using the Task Scheduler:

1.  Open the Task Scheduler.
2.  In the Task Scheduler window, click the "Create Basic Task" option in the Actions panel on the right.
3.  In the "Create Basic Task" wizard, enter a name and description for the task, and then click the "Next" button.
4.  Select the "Daily" option and specify the start date and time as 10:00 AM.
5.  Select the "Start a program" option and specify the path to the script.
6.  Review the task settings and click the "Finish" button to create the task.

The task will now be scheduled to run the script every day at 10:00 AM. 

### Elastic Search
Elasticsearch is a search engine based on the Lucene library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents.

Some basic terms related to text searches in Elasticsearch include:

-   Query: A request to search the index for documents matching a specific criteria.
-   Filter: A query that is used to narrow down the search results based on specific conditions. Filters are faster than queries because they do not affect the relevance score of the search results.
-   Full-text search: A search that looks for a specific string or phrase in the text of a document.
-   Index: A collection of documents that are similar in nature and are used for searching.
-   Mapping: The process of defining the fields and data types of an index.

Here are some basic examples of how to use Elasticsearch:

-   Search for documents containing the word "apple" in the field "description":

Copy code

```json
GET /my_index/_search
{
  "query": {
    "match": {
      "description": "apple"
    }
  }
}
```

Search for documents with a price between $10 and $20:

Copy code
```json
GET /my_index/_search
{
  "query": {
    "range": {
      "price": {
        "gte": 10,
        "lte": 20
      }
    }
  }
}
```

-   Search for documents containing the word "apple" in the field "description" and filter the results to only include documents with a price between $10 and $20:

```json
GET /my_index/_search
{
  "query": {
    "bool": {
      "must": {
        "match": {
          "description": "apple"
        }
      },
      "filter": {
 ```
 
 Elasticsearch and MongoDB are both NoSQL databases, but they have some differences in terms of their capabilities and use cases.

One key difference is that Elasticsearch is a search engine, while MongoDB is a document-oriented database. This means that Elasticsearch is optimized for search and analytics, while MongoDB is optimized for storing and retrieving large amounts of structured data.

Here are some other differences between Elasticsearch and MongoDB:

-   Elasticsearch is based on the Lucene library and provides full-text search and analytics capabilities, while MongoDB does not have built-in full-text search or analytics capabilities.
-   Elasticsearch stores data in JSON documents, while MongoDB stores data in binary JSON (BSON) documents.
-   Elasticsearch is horizontally scalable, meaning it can easily scale out to handle more traffic or data by adding more nodes to the cluster. MongoDB is also scalable, but it requires a more complex sharding setup to scale out.
-   Elasticsearch has a distributed architecture, meaning it stores and processes data across multiple servers. MongoDB also has a distributed architecture, but it uses a different approach called sharding to distribute data across multiple servers.

Here is an example use case for each database:

-   Elasticsearch: You want to build a search engine for a website that allows users to search for products by keyword and filter the results by price, brand, and other attributes. Elasticsearch would be a good choice because it provides fast full-text search and faceted filtering capabilities.
    
-   MongoDB: You want to build a social media application that stores user profiles, posts, and comments. MongoDB would be a good choice because it can store and retrieve large amounts of structured data efficiently.
    

In summary, Elasticsearch is generally better suited for search and analytics tasks, while MongoDB is better suited for storing and retrieving large amounts of structured data.

Elasticsearch is designed to be fast at search and analytics tasks, while MongoDB is designed to be fast at storing and retrieving large amounts of structured data.

In general, Elasticsearch is faster at search tasks because it uses a data structure called an inverted index, which allows it to search for documents containing a specific word or phrase very quickly. It is also optimized for real-time search and can return search results as soon as a document is indexed.

MongoDB is generally faster at inserting and retrieving large amounts of data because it uses a data structure called a B-tree index, which is optimized for these types of operations. It is also able to use memory-mapped files to access data, which can be faster than traditional file I/O.

Overall, the choice of which database to use depends on the specific needs of your application. If you need a fast search engine, Elasticsearch may be a good choice. If you need to store and retrieve large amounts of structured data, MongoDB may be a better choice.


-   Ngram search: You want to build a search engine for a website that allows users to search for products using partial keywords, such as "ipho" to find "iphone". You can use an ngram tokenizer to index the keywords in your product descriptions and enable partial matching.

```JSON
PUT /my_index
{
  "settings": {
    "analysis": {
      "analyzer": {
        "ngram_analyzer": {
          "type": "custom",
          "tokenizer": "ngram_tokenizer"
        }
      },
      "tokenizer": {
        "ngram_tokenizer": {
          "type": "ngram",
          "min_gram": 3,
          "max_gram": 3
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "analyzer": "ngram_analyzer"
      }
    }
  }
}
```

-   Highlighting: You want to display search results with the search keywords highlighted in the document text. You can use the highlighting feature to specify which fields should be highlighted and the formatting for the highlighted text.

```JSON
GET /my_index/_search
{
  "query": {
    "match": {
      "description": "iphone"
    }
  },
  "highlight": {
    "fields": {
      "description": {}
    }
  }
}
``` 

-   Aggregations: You want to analyze the sales data for your e-commerce website and generate reports on the top-selling products by category. You can use the aggregations feature to group and summarize the data by category and calculate the total sales for each group.

Copy code
```JSON
GET /sales/_search
{
  "size": 0,
  "aggs": {
    "products_by_category": {
      "terms": {
        "field": "category"
      },
      "aggs": {
        "total_sales": {
          "sum": {
            "field": "sales"
          }
        }
      }
    }
  }
}
```

ere are some other example use cases for Elasticsearch:

-   Real-time analytics: You want to track the performance of a website or application in real-time and visualize the data using a dashboard. You can use Elasticsearch to store and analyze the data in real-time and use a tool like Kibana to create the dashboard.
    
-   Log analysis: You want to analyze log data from multiple servers to troubleshoot issues or monitor the health of your systems. You can use Elasticsearch to store and analyze the log data and use a tool like Logstash to collect and process the logs.
    
-   Geospatial search: You want to build a search engine for a website that allows users to search for nearby restaurants, stores, or other points of interest. You can use Elasticsearch's geospatial capabilities to index the location data and perform searches based on distance from a given point.
    
-   Recommendation engine: You want to build a recommendation engine for an e-commerce website that suggests products to users based on their past purchases and browsing history. You can use Elasticsearch to store and analyze the user data and use machine learning techniques to generate recommendations.
    
-   Data lake: You want to build a data lake to store and analyze large volumes of structured and unstructured data from multiple sources. You can use Elasticsearch to index the data and provide fast search and analytics capabilities.

### Networking basics
TCP/IP (Transmission Control Protocol/Internet Protocol) is a set of networking protocols that define how computers communicate with each other over a network. Here are some basic TCP/IP terms and protocols:

-   IP (Internet Protocol): The IP protocol is responsible for routing packets of data between computers on a network. It defines the addressing scheme for computers on the network and how packets should be formatted and transmitted.
    
-   TCP (Transmission Control Protocol): The TCP protocol is responsible for establishing and maintaining connections between computers on a network and ensuring that data is transmitted reliably and in the correct order. It does this by using a three-way handshake to establish a connection, and by using error checking and retransmission to ensure reliable data transmission.
    
-   HTTP (Hypertext Transfer Protocol): HTTP is a application-level protocol that defines how web browsers and servers communicate with each other. It is used to request and transmit data over the internet, such as web pages, images, and other media.
    
-   FTP (File Transfer Protocol): FTP is a protocol for transferring files between computers on a network. It allows a client to connect to a server and upload or download files.
    
-   SMTP (Simple Mail Transfer Protocol): SMTP is a protocol for sending email messages between servers. It is used to transmit messages from the sender's mail server to the recipient's mail server.
    
-   DNS (Domain Name System): DNS is a system for mapping domain names (e.g. example.com) to IP addresses. It allows users to access websites and other resources using human-readable names instead of IP addresses.

#### Understanding HTTP
HTTP (Hypertext Transfer Protocol) is a protocol for transmitting data over the internet. It is the foundation of the modern web and is used by web browsers and servers to communicate with each other.

Here is how HTTP works:

1.  A client (such as a web browser) sends an HTTP request to a server. The request includes a method (e.g. GET, POST, PUT, DELETE) and a resource (e.g. a web page or an image).
2.  The server processes the request and sends back an HTTP response. The response includes a status code (e.g. 200 OK, 404 Not Found) and the requested resource or an error message.
3.  The client processes the response and displays the resource or handles the error.

There are several versions of HTTP, including HTTP/1.0, HTTP/1.1, and HTTP/2. Here are the main differences between these versions:

-   HTTP/1.0: This is the first version of HTTP and is the simplest. It does not support persistent connections, meaning that a new connection must be established for each request. It also does not support caching or request pipelining.
    
-   HTTP/1.1: This is an improved version of HTTP/1.0 that introduced several new features. It supports persistent connections, meaning that multiple requests can be sent over the same connection. It also supports caching, request pipelining, and chunked transfer encoding.
    
-   HTTP/2: This is a major revision of HTTP that introduces several new features and performance improvements. It supports multiplexing, meaning that multiple requests can be sent concurrently over the same connection. It also supports header compression, server push, and binary encoding.
    

In general, HTTP/2 is considered to be better than HTTP/1.1 because it is faster and more efficient. However, HTTP/1.1 is still widely used and is supported by all modern web browsers.

SSL/TLS uses a variety of algorithms to establish secure connections and encrypt data. These algorithms can be divided into three main categories:

-   Key exchange algorithms: These algorithms are used to establish a secure key exchange between the client and the server. Examples include RSA, DH (Diffie-Hellman), and ECDH (Elliptic Curve Diffie-Hellman).
    
-   Authentication algorithms: These algorithms are used to authenticate the server's identity to the client. Examples include RSA, DSA (Digital Signature Algorithm), and ECDSA (Elliptic Curve Digital Signature Algorithm).
    
-   Encryption algorithms: These algorithms are used to encrypt the data being transmitted between the client and the server. Examples include AES (Advanced Encryption Standard), DES (Data Encryption Standard), and RC4 (Rivest Cipher 4).
    

Some algorithms are considered more secure than others because they use longer keys or more complex algorithms. For example, AES is considered to be more secure than DES because it uses a longer key size (128, 192, or 256 bits). Similarly, RSA is considered to be more secure than DSA because it is based on the difficulty of factoring large composite numbers.

Some algorithms are considered vulnerable because they have known weaknesses or have been broken by attackers. For example, DES is considered to be vulnerable because it uses a relatively short key size (56 bits). Similarly, RC4 is considered to be vulnerable because it has a number of statistical biases that can be exploited by attackers.

In general, it is important to use strong algorithms to ensure the security of SSL/TLS connections.

SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are two protocols that are used to establish secure connections over the internet. They are both based on the same underlying technology, but they have some differences in their design and implementation.

Here are the main differences between SSL and TLS:

-   Version: SSL is the older of the two protocols, with versions ranging from SSLv1 to SSLv3. TLS is the newer protocol, with versions ranging from TLSv1 to TLSv1.3.
    
-   Compatibility: SSL is not compatible with TLS, meaning that SSL clients cannot communicate with TLS servers and vice versa.
    
-   Security: SSL has a number of known vulnerabilities, such as the POODLE attack and the FREAK attack. TLS is designed to be more secure and has fewer known vulnerabilities.
    
-   Performance: TLS is generally considered to be faster and more efficient than SSL because it uses more modern encryption algorithms and has fewer overhead costs.
    

In summary, TLS is the successor to SSL and is the recommended protocol for establishing secure connections over the internet. It is widely used by protocols such as HTTPS (HTTP Secure), SMTP (Simple Mail Transfer Protocol), and FTP (File Transfer Protocol).


#### How to check My IP 
If you want to programmatically check your IP address using an API, you can use a service like [https://ipify.org](https://ipify.org/). This service provides a simple API that returns your public IP address as a string in JSON format. For example:
    
```curl
$ curl https://api.ipify.org
192.168.1.101`
```

### Encryption 
Encryption is a method of converting plaintext data into a form that cannot be read by anyone who does not have the decryption key. The purpose of encryption is to protect the confidentiality of data by making it unreadable to unauthorized parties.

Here are a few examples of encryption algorithms:

-   AES (Advanced Encryption Standard): AES is a symmetric encryption algorithm that is widely used to secure data in transit and at rest. It uses a fixed-size key to encrypt and decrypt data and is considered to be very secure.
    
-   RSA (Rivest-Shamir-Adleman): RSA is an asymmetric encryption algorithm that is used to secure data in transit. It uses a pair of keys (a public key and a private key) to encrypt and decrypt data. The public key is used to encrypt the data, and the private key is used to decrypt it.
    
-   Blowfish: Blowfish is a symmetric encryption algorithm that is fast and secure. It uses a variable-size key to encrypt and decrypt data.
    

Checksum is a method of verifying the integrity of data by calculating a numerical value based on the data and storing it with the data. The purpose of a checksum is to detect any changes or errors in the data by comparing the stored checksum with a newly calculated checksum.

Here are a few examples of checksum algorithms:

-   MD5 (Message Digest Algorithm 5): MD5 is a widely used checksum algorithm that produces a 128-bit hash value. It is fast and relatively secure, but it is vulnerable to collision attacks.
    
-   SHA (Secure Hash Algorithm): There are several versions of SHA, including SHA-1, SHA-2, and SHA-3. SHA is a secure checksum algorithm that produces a hash value of different sizes depending on the version.
    
-   CRC (Cyclic Redundancy Check): CRC is a checksum algorithm that is used to detect errors in data transmission. It produces a fixed-size checksum based on the data and a predefined polynomial.
 
In summary, encryption is used to protect the confidentiality of data by making it unreadable, while checksum is used to detect errors or changes in data by comparing a stored value with a newly calculated value.
Symmetric key algorithms, also known as secret key algorithms, use the same key to encrypt and decrypt data. This means that the sender and receiver of the data must share the same key in order to communicate securely. Examples of symmetric key algorithms include AES (Advanced Encryption Standard), Blowfish, and DES (Data Encryption Standard).

Here is an example of how symmetric key encryption works:

1.  The sender wants to send a message to the receiver.
2.  The sender and receiver agree on a secret key to use for encryption and decryption.
3.  The sender uses the secret key to encrypt the message.
4.  The sender sends the encrypted message to the receiver.
5.  The receiver uses the secret key to decrypt the message.

Asymmetric key algorithms, also known as public key algorithms, use a pair of keys (a public key and a private key) to encrypt and decrypt data. The public key is used to encrypt the data, and the private key is used to decrypt it. This means that the sender and receiver do not have to share the same key in order to communicate securely. Examples of asymmetric key algorithms include RSA (Rivest-Shamir-Adleman) and Diffie-Hellman.

Here is an example of how asymmetric key encryption works:

1.  The sender wants to send a message to the receiver.
2.  The receiver generates a public key and a private key.
3.  The receiver sends the public key to the sender.
4.  The sender uses the public key to encrypt the message.
5.  The sender sends the encrypted message to the receiver.
6.  The receiver uses the private key to decrypt the message.

In summary, symmetric key algorithms use the same key for encryption and decryption, while asymmetric key algorithms use a pair of keys for encryption and decryption.

#### Man in the middle
A man-in-the-middle (MITM) attack is a type of cyber attack where an attacker intercepts communication between two parties and disguises themselves as one of the parties to steal sensitive information or manipulate the communication.

Here is an example of how an MITM attack might work:

1.  The attacker intercepts communication between a client (such as a web browser) and a server.
2.  The attacker disguises themselves as the server and sends a fake SSL/TLS certificate to the client. The fake certificate contains the attacker's own public key and other information about the server's identity.
3.  The client verifies the fake certificate and establishes an SSL/TLS connection with the attacker.
4.  The client sends sensitive information (e.g. login credentials) to the attacker, who intercepts and steals it.
5.  The attacker forwards the information to the server, disguising themselves as the client. The server processes the information and sends back a response, which the attacker intercepts and forwards to the client.

An MITM attack can be successful if the client trusts the fake certificate and establishes a connection with the attacker.

#### Digtial Ceritificate
An SSL/TLS (Secure Sockets Layer/Transport Layer Security) certificate is a digital certificate that is used to establish trust and secure connections over the internet. It is used by protocols such as HTTPS (HTTP Secure) to authenticate the server's identity and establish an encrypted connection with the client.

Here is how an SSL/TLS certificate generates trust:

1.  The server generates a certificate signing request (CSR) and submits it to a certificate authority (CA). The CSR contains information about the server's identity, such as its domain name, organization name, and location.
    
2.  The CA verifies the server's identity and issues an SSL/TLS certificate. The certificate contains the server's public key and other information about the server's identity.
    
3.  The client (such as a web browser) receives the SSL/TLS certificate from the server. The client verifies the certificate using the CA's public key, which is stored in the client's trust store.
    
4.  If the certificate is valid and trusted, the client establishes an SSL/TLS connection with the server. The connection is encrypted using the server's public key and the client's private key.
    

A certificate authority (CA) is a trusted third party that issues SSL/TLS certificates to organizations and websites. CAs are responsible for verifying the identity of the organizations and websites that request certificates and for issuing certificates that are trusted by clients.

Certificate chaining is the process of linking multiple SSL/TLS certificates to form a chain of trust. This is typically used when an intermediate certificate authority (CA) is used to issue a certificate on behalf of a root CA. The intermediate CA's certificate is chained to the root CA's certificate, establishing a trust chain that can be verified by the client.

In summary, an SSL/TLS certificate generates trust by being issued by a trusted certificate authority and being verified by the client using the CA's public key. Certificate chaining is used to establish a trust chain between multiple CAs, allowing clients to trust intermediate CAs that are issued by root CAs.


