# Backend-Development Technologies

## Table of Contents

* [Introduction](#introduction)
* [Overview](#overview)
* [Node.js Vs PHP](#nodejs-vs-php)
  * [What is Node JS?](#what-is-node-js)
  * [What is PHP?](#what-is-php)
  * [Comparison according to different features](#comparison-according-to-different-features)
    * [Leverage real-time experience](#leverage-real-time-experience)
    * [Faster Server Connection](#faster-server-connection)
    * [Flexibility](#flexibility)
    * [Hosting](#hosting)
    * [Coding](#coding)
    * [Performance](#performance)
    * [Security](#security)
    * [Frameworks](#frameworks)
    * [Community](#community)
    * [Ecosystem](#ecosystem)
    * [When to Choose Node JS Over PHP](#when-to-choose-node-js-over-php)
    * [When to Choose PHP Over Node JS](#when-to-choose-php-over-node-js)
* [References](#references)    

<!-- ---------------------------------------------------------------------- -->

## Introduction

Backend development is the unsung hero of the digital world. Think of it as the engine of a car, it's invisible to the passengers but crucial for the car to function.

Backend technologies are the programming languages, frameworks, and databases that developers use to build the server-side logic of an application. This includes everything from processing user requests, managing data storage, and ensuring security to powering the features users see on the front end.

In essence, backend development is about building the foundation upon which the user experience is constructed. It's the backbone that supports the entire application, making it efficient, scalable, and secure.

Node.js and PHP are two prominent backend technologies used for web application development.
This study aims to compare and contrast these technologies across various dimensions, including performance, scalability, development experience, and their application in API development. 

<!-- ---------------------------------------------------------------------- -->
## Overview

The popularity of JavaScript has surged since its invention, giving Node.js developers a wide range of frameworks like Vue, Meteor, Angular, React, Express, and more to choose from. Deciding on the best option for a project can be challenging. Node JS and PHP are both powerful choices for backend development, sparking debate in the developer community. PHP has a long history as one of the most widely used technologies, while NodeJS allows for backend programming using JavaScript. Choosing between PHP and NodeJS can be tough, as businesses and developers worldwide struggle to assess the strengths of Node.js compared to other backend technologies.

<!-- ---------------------------------------------------------------------- -->
## Node.js Vs PHP

### What is Node JS?

Node.js is an open-source runtime environment that allows you to run JavaScript programs on the server side, making it great for building fast and scalable applications. It utilizes an event-driven, non-blocking I/O model for optimal performance. Previously, JavaScript was mainly used for frontend development in web browsers, but Node.js has revolutionized this by allowing asynchronous JavaScript development with the Chrome’s V8 JavaScript engine. This has elevated JavaScript to the level of more powerful languages like Python. With Node.js, you can create amazing websites and perform various tasks, similar to Python. Node.js also provides excellent support for JSON, enabling communication with NoSQL databases. Big companies like Microsoft, LinkedIn, and PayPal utilize Node.js for enterprise product development to improve resource utilization, scalability, and revenue.

### What is PHP?

PHP (Hypertext Processor) is open-source server-side scripting language, was created by Rasmus Lerdorf in 1994. It is heavily used by popular websites like Wikipedia, Tumblr, and Facebook. According to a survey by W3Tech, PHP is used in nearly 79% of websites. It is also widely embraced by CMS platforms like Shopify, WordPress, Drupal, and WooCommerce. Despite being synchronous and dependent on a central server, PHP offers various built-in features and packages that simplify the development of eCommerce and CMS websites. 

### Comparison according to different features

#### Leverage real-time experience

Enabling high-performance apps with features like streaming, real-time chatting, and event-driven JavaScript environment for transactions.
Node.js excels in creating real-time applications with its event-driven, non-blocking architecture. It efficiently handles multiple concurrent connections, perfect for real-time interactions.

- Example:

Imagine a simple chat application. Users can join a chat room, send messages, and receive messages instantly from other users in the same room. This is a classic example of a real-time application that can be built efficiently using Node.js.

- How it works in Node js:

1. Server-Side (Node.js):

    * A Node.js server is set up using Express.js for routing and Socket.IO for real-time communication.

    * When a user connects to the server, Socket.IO establishes a persistent connection.

    * The server maintains a list of connected users and their respective chat rooms.

    * When a user sends a message, the server broadcasts it to all users in the same chat room.

2. Client-Side (Browser):

    * The client-side application (typically built with JavaScript, HTML, and CSS) establishes a WebSocket connection to the server using Socket.IO.

    * When a user sends a message, it's sent to the server via the WebSocket connection.

    * The server broadcasts the message to all connected clients in the same chat room.

    * Each client updates its chat interface with the newly received message.

```
        const express = require('express');
        const http = require('http');
        const socketIo = require('socket.io');

        const app = express();
        const server = http.createServer(app);
        const   
        io = socketIo(server);

        io.on('connection', (socket)   
        => {
        console.log('a user connected');
        socket.on('chat message', (msg) => {
            io.emit('chat message', msg);
        });
        });

        server.listen(3000, () => {
        console.log('listening on *:3000');   

        });

```
- Key points:

   * Socket.IO: Handles the real-time communication between the server and clients.

   * Event-driven: The server listens for 'connection' and 'chat message' events.

   * Broadcasting: The io.emit function broadcasts messages to all connected clients.

- PHP with Pusher (External Service)

1. Server-Side (PHP):

```
<?php

require 'vendor/autoload.php';

$pusher = new Pusher\Pusher("your_app_id", "your_app_key", "your_app_secret", ['cluster' => 'your_cluster']);

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  $message = $_POST['message'];
  $pusher->trigger('chat', 'new-message', $message);
}

?>

<!DOCTYPE html>
<html>
<head>
  <title>Chat Room</title>
  <script src="https://js.pusher.com/7.2.0/pusher.min.js"></script>
  <script>
    const pusher = new Pusher('your_app_key', {
      cluster: 'your_cluster'
    });

    const chatChannel = pusher.subscribe('chat');

    chatChannel.bind('new-message', function(data) {
      // Update chat interface with received message
    });

    const messageForm = document.getElementById('message-form');
    messageForm.addEventListener('submit', function(e) {
      e.preventDefault();
      const   
 message = document.getElementById('message-input').value;
      // Send message to PHP script using AJAX or form submission
    });
  </script>
</head>
<body>
  <h1>Chat Room</h1>
  <div id="chat-messages"></div>
  <form id="message-form">
    <input type="text" id="message-input" placeholder="Enter message">
    <button type="submit">Send</button>
  </form>   

</body>
</html>

```
This approach uses PHP for the backend logic and a third-party service like Pusher for real-time communication.

2. Client-Side (Browser):

This stays mostly the same as the Node.js example, with the JavaScript code connecting to Pusher instead of a local server.

- Analysis:

   - PHP: Requires an external service like Pusher for real-time communication, adding complexity and cost.

   - Node.js: Handles real-time communication directly through WebSockets, eliminating the need for external services.

- Advantages of Node.js for Real-Time Applications

   - Built-in WebSockets: Node.js natively supports WebSockets, facilitating real-time connections.

   - Event-Driven Architecture: Well-suited for handling multiple concurrent connections and real-time events efficiently.

   - Scalability: Node.js applications can scale easily to handle increasing traffic.

- Limitations of PHP for Real-Time Applications

  - Reliance on External Services:Requires additional setup and potential costs for services like Pusher.

  - Increased Complexity: Handling real-time communication in PHP often involves more complex code and libraries.

  - Less Scalable: PHP applications can struggle with high volumes of concurrent connections in real-time scenarios.

This is a basic example. Real-world chat applications would involve additional features like user authentication, private messaging, group chats, and more. However, this demonstrates the core concept of real-time communication using Node.js and Socket.IO.

#### Faster Server Connection

Node.js allows for the creation of non-blocking I/O JavaScript applications with an event queue that can handle multiple requests simultaneously, making it highly scalable. By leveraging JavaScript's inherent asynchrony, Node.js optimizes CPU and memory usage while managing more requests than traditional multithreaded servers. This makes Node.js well-suited for real-time applications with numerous I/O operations. In comparison, Node.js is asynchronous, event-driven, and non-blocking, while PHP is synchronous. Node.js is therefore considered a superior choice for accelerating development compared to PHP at this point.

- Example: A Web Server

  - Traditional Synchronous Server (PHP):

  *  Each incoming request creates a new thread.

  *  If a request involves I/O, the thread is blocked until the operation completes, preventing it from handling other requests.

  *  With many concurrent requests, resource consumption increases significantly.

- Node.js Server:

  *  A single thread handles multiple requests concurrently.

  *  When an I/O operation is initiated, the request is added to the event queue.

  *  The server continues processing other requests while waiting for the I/O to complete.

  *  Once the I/O operation finishes, its callback is added to the event queue and executed when its turn comes.

  *  In essence, Node.js can handle thousands of concurrent connections with a single thread, making it highly efficient and scalable for applications like web servers, chat applications, and real-time data processing.


- PHP's Approach: Limitations

      While PHP has improved over the years, it still primarily follows a synchronous model. This means that when a PHP script encounters an I/O operation (like fetching data from a database), it pauses execution until the operation completes. This can lead to performance bottlenecks, especially under high traffic.

      While PHP frameworks like Laravel and Symfony have introduced asynchronous features, they often rely on external libraries or components, making the implementation more complex.

- Example:

A simple PHP script handling multiple requests without optimization:
```
<?php
// Simulate a long-running task (e.g., database query)
function processRequest() {
  sleep(2); // Simulate a 2-second delay
  echo "Request processed\n";
}

for ($i = 0; $i < 10; $i++) {
  processRequest();
}
?>  
```
This script will take approximately 20 seconds to complete, as each request is processed sequentially.

- The Synchronous Nature

The key point is that the code executes sequentially. This means:

* The first call to processRequest finishes completely (including the 2-second delay) before the second call starts.

* The second call waits for its 2 seconds before the third starts, and so on.

* Imagine a queue of people: Each person is a request. The first person (request) must finish their task before the next person can start. This is synchronous processing.

- Node.js Advantage: Asynchronous Handling

```
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
  // Simulate asynchronous file reading
  fs.readFile('large_file.txt', 'utf8', (err, data) => {
    if (err) {
      res.writeHead(500, {'Content-Type': 'text/plain'});
      res.end('Error reading file');
    } else {
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end(data);
    }
  });
});

server.listen(3000, () => {
  console.log('Server listening on port 3000');
});

```

- How Asynchronous Behavior Works

The key to understanding this code lies in the asynchronous nature of fs.readFile. When a request comes in:

  * The server starts handling the request.

  * It initiates the file reading using fs.readFile.

  * Instead of waiting for the file to be read completely, the server continues to handle other incoming requests.

Once the file is read (or an error occurs), the callback function provided to fs.readFile is executed.

The response is sent to the original client.This asynchronous pattern allows the server to efficiently handle multiple requests concurrently without blocking the main thread while waiting for file I/O operations to complete.

<img src="https://www.simform.com/wp-content/uploads/2020/10/NodejsvsPHPSpeed.jpeg" width="700" height="300">

#### Flexibility

Both Node.js and PHP offer flexibility, but in slightly different ways. Node.js shines with its extensive package ecosystem and focus on JavaScript, while PHP offers built-in functionality and allows for a wider range of tools based on the project's needs. Picking the best technology depends on the specific requirements of your application.

- Here's a PHP example demonstrating flexibility:

```
<?php

// Example 1: Using different routing approaches

// 1. Manual routing with switch statement
$endpoint = $_SERVER['REQUEST_URI'];
switch ($endpoint) {
  case '/users':
    // Handle users endpoint logic
    break;
  case '/products':
    // Handle products endpoint logic
    break;
  default:
    echo "404 Not Found";
}

// 2. Using a lightweight framework like Slim (requires installation)
use Slim\Slim;

$app = new Slim();
$app->get('/users', function ($request, $response) {
  // Handle GET requests for users
});
$app->post('/products', function ($request, $response) {
  // Handle POST requests for products
});
$app->run();

// Example 2: Using different libraries for tasks

// 1. Form validation with built-in functions
$name = $_POST['name'];
if (empty($name)) {
  echo "Error: Name is required";
  exit;
}

// 2. Form validation with a library like Symfony Validator (requires installation)
use Symfony\Component\Validator\Constraints as Assert;
use Symfony\Component\Validator\Validation;

$validator = Validation::createValidator();   

$errors = $validator->validate($name, [
  new Assert\NotBlank(),
]);

if (count($errors) > 0) {
  // Handle validation errors
  foreach ($errors as $error) {
    echo $error->getMessage() . "<br>";
  }
  exit;
}

// Example 3: Using different database libraries

// 1. Using PDO for manual database interaction
$dsn = 'mysql:host=localhost;dbname=mydatabase';
$username = 'your_username';
$password = 'your_password';

try {
  $db = new PDO($dsn, $username, $password);
  // Execute database queries
} catch (PDOException $e) {
  echo "Error: " . $e->getMessage();
}

// 2. Using a database abstraction layer like Doctrine (requires installation)
use Doctrine\ORM\EntityManager;
use Doctrine\ORM\Tools\Setup;

$paths = array(SRC_PATH . '/Entity');
$isDevMode = true;

$dbConfigs = Setup::createConfiguration($isDevMode);
$dbConfigs->setMetadataSources(array(Setup::ANNOTATIONS));
$dbConfigs->setEntityManagerName('default');
$dbConfigs->setSQLAccessMode('READ_WRITE');
$dbConnection = array(
  'driver' => 'pdo_mysql',
  'host' => 'localhost',
  'dbname' => 'mydatabase',
  'user' => 'your_username',
  'password' => 'your_password',
);

$entityManager = EntityManager::create($dbConnection, $dbConfigs);

// ... use the EntityManager for database operations

// These examples showcase how PHP allows various approaches to achieve similar goals.
?>
```

- Explanation:

  - This code demonstrates flexibility in routing approaches: using a switch statement or a lightweight framework like Slim.
  
  - It shows the ability to use different libraries for tasks like form validation (built-in functions or external libraries like Symfony Validator).

  - It highlights the option to utilize various database libraries (PDO or Doctrine) based on your preference.

Node.js is flexible and allows development with any technology, without strict rules. NPM enables smooth and quick app development.

- Example:

```
    const express = require('express');
    const app = express();

    // Example of using different middleware and routing
    app.use(express.json()); // Parse JSON request bodies
    app.get('/users', (req, res) => {
    // Handle GET requests for users
    });
    app.post('/users', (req, res) => {
    // Handle POST requests for users
    });
```

The code utilizes Express.js, a popular framework for building web applications in Node.js. However, this is just one option.Node.js allows you to use other frameworks like Koa.js, Hapi.js, or even build your server logic from scratch with minimal libraries. You're not restricted to a specific framework.

1. NPM Ecosystem:

The code snippet includes express.json(). This middleware function comes from the express package, readily available on NPM. Node.js leverages the vast NPM ecosystem. You can find numerous packages for various functionalities like database access, authentication, templating, or real-time communication. This eliminates the need to reinvent the wheel for common tasks and allows customization based on your specific needs.

2. Freedom in Development Style:

The code demonstrates basic routing using app.get and app.post. However, Node.js allows for more complex routing patterns with Express.js or other libraries.

You can structure your code in different ways, using object-oriented or functional programming paradigms, or a combination of both. Node.js doesn't impose a rigid coding style.


#### Hosting

While both Node.js and PHP can be hosted on various platforms, Node.js often demands more control over the server environment. This can lead to higher initial costs but also offers greater flexibility and performance potential. PHP, on the other hand, is generally more accessible for smaller projects due to wider hosting compatibility and often lower costs.

- Node.js:

  - Requires a runtime environment: Node.js needs to be installed on the server.
    
  - Flexible hosting options: Can run on VPS, dedicated servers, cloud platforms, or even shared hosting if supported.

  - Often requires more control: Users often need root access to install dependencies and configure the environment.   

  - Requires a server environment, which can incur costs for VPS, dedicated servers, or cloud platforms.
  Can be more expensive for smaller projects due to the need for more control over the server.

- PHP:

  - Typically embedded in web servers: PHP scripts are often executed by web servers like Apache or Nginx.

  - Wider hosting compatibility: More hosting providers support PHP due to its long-standing popularity.

  - Less demanding on server configuration: PHP is generally easier to set up on shared hosting environments.

  - Often included in shared hosting packages, making it more affordable for small to medium-sized projects.
  Can become more expensive as traffic grows and requires additional resources.

#### Coding

Node.js often requires explicit code for asynchronous operations, improving code organization and readability. It utilizes JavaScript's functional programming, resulting in concise code in some instances. 

PHP is traditionally imperative, leading to shorter code blocks for simple tasks but becoming verbose for complex logic and large-scale applications. It's misleading to generalize that one language consistently produces shorter code than the other, as both Node.js and PHP can be written in concise or verbose styles based on the developer and task at hand.

#### Performance

Performance metrics in PHP or Node.js gauge code efficiency and impact on key performance indicators (KPIs) such as page loads. Improving technology performance leads to better UX through optimized KPIs.

- Node Js

Node.js with JavaScript V8 Engine offers fast execution and startup time due to its asynchronous nature. Being event-driven, Node.js does not block requests, allowing for concurrent module execution. This means multiple modules can be executed at the same time, although not simultaneously, resulting in varying beginning and completion times even when using the same resource and environment.

- PHP

PHP, developed earlier, lacks page-load efficiency due to blocking processes until fully calculated, resulting in slow loading without concurrency. However, pairing PHP with HHVM Virtual Machine can enhance performance by 75%. Despite this, Node.js remains a faster alternative for web applications.

#### Security
When comparing PHP and Node.js in terms of security, it's important to consider their inherent features, ecosystems, common vulnerabilities, and best practices.

-   PHP

Strengths:

1\. Mature Ecosystem:

\- PHP's long history has resulted in a stable ecosystem with a plethora of tools, frameworks (such as Laravel and Symfony), and libraries that have been extensively tested.

2\. Built-in Security Functions:

\- PHP provides built-in functions for tasks like data sanitization and encryption, such as \`htmlspecialchars\` and \`password_hash\`.

3\. Extensive Community and Resources:

\- The large PHP community offers abundant resources, documentation, and pre-vetted libraries focused on security.

Weaknesses:

1\. Historical Vulnerabilities:

\- PHP applications have often faced issues like SQL injection, XSS, and CSRF, primarily due to poor coding practices and a lack of security awareness.

2\. Inconsistent Updates:

\- Many older PHP applications run on outdated versions, missing the latest security patches due to the effort required to update legacy codebases.

3\. Configuration Issues:

\- PHP's flexibility can lead to security misconfigurations, especially if default settings are not adjusted by inexperienced developers.

-   Node.js

Strengths:

1\. Modern Development Practices:

\- Node.js promotes non-blocking, event-driven architecture, which can help mitigate certain types of attacks, such as Denial of Service (DoS).

2\. Robust Package Management:

\- npm, Node.js's package manager, offers many security-focused packages and tools, like Helmet for securing Express apps.

3\. Active Security Initiatives:

\- The Node.js community actively promotes security best practices and has a Security Working Group dedicated to addressing security issues.

Weaknesses:

1\. Dependency Management Risks:

\- Heavy reliance on third-party packages can introduce vulnerabilities if these packages are not properly managed and updated.

2\. Common Vulnerabilities:

\- Node.js applications are still susceptible to common web vulnerabilities like XSS, CSRF, and injection attacks if not properly addressed.

3\. Rapid Ecosystem Changes:

\- The fast-evolving JavaScript ecosystem can make it difficult to keep up with security updates and best practices.

**Best Practices for Both PHP and Node.js:**

1\. Regular Updates:

\- Ensure that your runtime, dependencies, and libraries are always up-to-date with the latest security patches.

2\. Code Reviews and Audits:

\- Conduct regular code reviews and security audits to identify and address vulnerabilities.

3\. Input Validation and Sanitization:

\- Validate and sanitize all user inputs to prevent injection attacks and other input-based vulnerabilities.

4\. Use Security Libraries:

\- Employ established security libraries and frameworks that offer built-in protections.

5\. Secure Configuration:

\- Follow security best practices for server and application configurations, including using HTTPS, proper session management, and secure cookie settings.



#### Frameworks

Frameworks provide pre-written code for common functions, libraries, and APIs, allowing you to focus on project specifics. A comprehensive framework reduces redundant code, streamlining development efforts.

- Node Js

Node.js has experienced significant growth in libraries. Frameworks like Meteor, Derby, Express, and Sails, lead to increased productivity and reduced development time. However, PHP still has a much larger number of frameworks compared to Node.js.

- PHP

PHP boasts various specialized frameworks like Laravel, CodeIgniter, CakePHP, and Phalcon, popular among development agencies due to their rich libraries and niche markets.

Choosing between Node.js and PHP often boils down to project requirements, team expertise, and long-term goals. Both ecosystems offer powerful frameworks to streamline development.

#### Community

The community's strength and expertise determine the updates for frameworks, libraries, and projects in each technology. Teams cannot code every feature from scratch, so using popular libraries saves time and boosts productivity. The quality of individual projects is more important than the number of projects in a large community, as it adds value to the team.

- Node Js

Node.js projects are mostly found on npmjs.com registry. Despite a smaller community compared to PHP, the community focuses on creating projects that cater to current development needs. Projects often aim to enhance Node.js with unique features, rather than just serving as feature-importing libraries from other languages.

- PHP

PHP, with its long history, boasts a sizable community and a vast number of projects. However, newer projects by the community may seem uninspiring compared to Node.js. Initially well-received for enhancing platform features, PHP projects now face competition and calls for more innovative ideas.

#### Ecosystem

A platform's ecosystem relies on its community, who contribute open-source libraries, APIs, modules, frameworks, and projects at any given time to show its vitality.

- Node Js

While Node.js offers many advantages, its asynchronous programming model and the flexibility it provides can sometimes lead to code that is:

  *  Difficult to reason about: The non-blocking nature and callback-based approach can make code harder to follow and debug compared to traditional synchronous languages.

  * Prone to errors: Improper handling of asynchronous operations can result in unexpected behavior and errors.

  * Steeper learning curve: Developers new to Node.js might find it challenging to grasp the asynchronous paradigm and write efficient code.

**Example:**

```
fs.readFile('file1.txt', (err, data) => {
  if (err) throw err;
  fs.readFile('file2.txt', (err, data2) => {
    if (err) throw err;
    // Process data
  });
});

```
  - fs.readFile(): This function is used to read the contents of a file asynchronously.

  - Callback function: The second argument passed to fs.readFile is a callback function that will be executed once the file reading operation is complete.

  - Nested callback: The second fs.readFile is nested inside the first callback, creating a pyramid-like structure.

  - Error handling: The if (err) throw err statements handle potential errors during file reading.

- Why is this a problem?

  - Readability: As the number of nested callbacks increases, the code becomes increasingly difficult to follow and understand.

  - Maintainability: Making changes to this code can be error-prone and time-consuming due to its complexity.

  - Error handling: Managing errors in multiple levels of nested callbacks can be challenging.

To avoid callback hell, Node.js developers often use techniques like Promises, async/await, or libraries like Async. These approaches help to flatten the code structure and make it more readable and maintainable.

This code demonstrates the potential for callback hell in Node.js, highlighting the need for proper error handling and asynchronous flow management.

- PHP

WordPress has had a significant impact on the PHP ecosystem, powering a large portion of websites online. This demonstrates PHP's widespread influence. The PHP community has created sample resources and technology to support new developers and facilitate their onboarding process.

Both ecosystems have their strengths and weaknesses.

#### When to Choose Node JS Over PHP?

Prefer Node.js over PHP for enterprise web development for specific features, stick to PHP otherwise.

1. **Development Efficiency:** Node.js is commonly used with MongoDB, ExpressJS, and AngularJS for developing dynamic single-page applications. It enhances development ease and performance in this stack.

2. **High Speed and Consistent Callback from Servers:** Node.js web apps excel in performance by maintaining constant server requests. Its non-blocking asynchronous design boosts speed, making it ideal for quick-paced Real-time applications.

#### When to Choose PHP Over Node JS?

PHP is recommended for web applications desiring certain properties in their technology stack.

1. **Centralized Server and No Scaling Needs:**

PHP is ideal for a single centralized server setup for your web application. It complements well with Linux, Apache, and MySQL.

2. **Portability:**

PHP allows for great portability among servers, enabling you to easily transfer your web application to servers with Apache, IIS, and database support. When integrated with CMS like WordPress, Joomla, or Drupal, you can quickly launch your website. Although PHP limits the number of servers you can connect with, its versatility makes it a popular choice for web development.

Wikipedia, MailChimp, and Tumblr showcase PHP's versatility for building websites and utilizing centralized servers effectively.


So it all depends on the requirements of you Project.

<!-- ---------------------------------------------------------------------- -->
## References

* [RadixWeb](https://radixweb.com/blog/node-js-vs-php)
* [SIMFORM](https://www.simform.com/blog/nodejs-vs-php/)
* [MoldStud](https://moldstud.com/articles/p-the-role-of-php-in-content-management-systems-cms-development#:~:text=PHP%20is%20known%20for%20its%20simplicity%2C%20flexibility%2C%20and%20robustness%2C,web%20applications%20such%20as%20CMS.)
* [Kinsta](https://kinsta.com/blog/node-js-vs-php/)
