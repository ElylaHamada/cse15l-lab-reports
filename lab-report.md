# Lab report 2

## Part 1
__Answer the following questions for each of the screenshots:__
1. which methods in your code are called?
2. what are the relevant arguments to those methods, and the values of any relevant fields of this class?
3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
<img width="909" alt="Screenshot 2024-04-24 at 20 38 45" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/1d2c8ad9-cfe4-487f-963b-61357ba09e1e">

_Question 1_

The methods in my code that were called were the main method and within the main method, the Server.start method was called which creates an instance of the HttpServer class and sets up the server to listen on the specified port. When a request is received, the handle method of the ServerHttpHandler is called. This method is responsible for processing the request and generating the response.Inside the handle method, the handleRequest method of the Handler class is called. This method is responsible for handling the specific request path and returning the appropriate response. In the Handler class, the handleRequest method checks if the request path contains "/add-message". If it does, it further processes the query parameters "s" and "user" to extract the message and user information.

_Question 2_
> __handleRequest method in the Handler class:__
- Argument: URI url
- Fields used: num (an integer field), chatHistory (an ArrayList of strings)
> __handle method in the ServerHttpHandler class:__
- Argument: HttpExchange exchange
- Fields used: handler (an instance of the URLHandler interface)
> __start method in the Server class:__
- Arguments: int port and URLHandler handler
> __main method in the ChatServer and NumberServer classes:__
- Argument: String[] args
  
_Question 3_

The values of the num field and the chatHistory field in the Handler class could potentially change based on the specific request /add-message?s=Hello&user=jpolitz. If the request involves adding the message "Hello" from the user "jpolitz" to the chat history, these fields may get updated. 
<img width="909" alt="Screenshot 2024-04-24 at 20 38 24" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/8b00dd7e-1aa2-4338-962b-be409e1ba608">

_Question 1_

The methods in my code that were called were the main method and within the main method, the Server.start method was called which creates an instance of the HttpServer class and sets up the server to listen on the specified port. When a request is received, the handle method of the ServerHttpHandler is called. This method is responsible for processing the request and generating the response.Inside the handle method, the handleRequest method of the Handler class is called. This method is responsible for handling the specific request path and returning the appropriate response. In the Handler class, the handleRequest method checks if the request path contains "/add-message". If it does, it further processes the query parameters "s" and "user" to extract the message and user information.

_Question 2_

> __handleRequest method in the Handler class:__
- Argument: URI url
- Fields used: num (an integer field), chatHistory (an ArrayList of strings)
> __handle method in the ServerHttpHandler class:__
- Argument: HttpExchange exchange
- Fields used: handler (an instance of the URLHandler interface)
> __start method in the Server class:__
- Arguments: int port and URLHandler handler
> __main method in the ChatServer and NumberServer classes:__
- Argument: String[] args
- 
_Question 3_

The values of the num field and the chatHistory field in the Handler class could potentially change based on the specific request /add-message?s=Hello&user=jpolitz. If the request involves adding the message "Hello" from the user "jpolitz" to the chat history, these fields may get updated. 

## Part 2

On the command line of your computer, run ls with the absolute path to the private key for your SSH key for logging into ieng6.ls


On the command line of the ieng6 machine, run ls with the absolute path to the public key for your SSH key for logging into ieng6 (this is the one you copied to your account on ieng6 using ssh-copy-id, so it should be a path on ieng6's file system).

A terminal interaction where you log into your ieng6 account without being asked for a password.


## Part 3

One of the first things I learned from weeks 2 and 3 that was very new to me was learning about ssh keys and how to use them. The analogy given to us during the lab about our home and our dog living inside the home  how this analogy explained how public and private keys work with the SSH system made it so much easier to understand. What the analogy basically explained was that our home is the server and the dog is inside our home. The analogy here is how the home is the ssh system, the clothes we have inside the house that lets the dog detect who we are is our public key, and the dog matches the scent of our clothes inside our home to our sc ent is basically the ssh system matching the private key to our public key that we sent to, for example, our ieng6 server with the ssh-copy-id. This analogy helps me easily understand how the SSH system works and how we use both the public and private keys into the server to verify our identity. 
