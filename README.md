# Simple Load Balancer Implementation in Go

This Go project demonstrates a simple load balancer implementation using a round-robin strategy. Let's break down the components and functionalities:

## Server Interface

- This interface defines the methods required for a server:
  - `Address() string`: Returns the address of the server.
  - `IsAlive() bool`: Checks if the server is alive.
  - `Serve(rw http.ResponseWriter, r *http.Request)`: Serves HTTP requests.

## SimpleServer Struct

- Implements the `Server` interface.
- Contains an address and a reverse proxy for forwarding requests.
- `newSimpleServer`: Constructs a new `simpleServer` instance.

## LoadBalancer Struct

- Manages a pool of servers and distributes requests among them.
- Keeps track of the current round-robin count.
- Provides a method `getNextAvailableServer()` to fetch the next available server based on the round-robin strategy.
- `NewLoadBalancer`: Constructs a new `LoadBalancer` instance.

## handleErr Function

- Handles errors by printing them and exiting the program if an error occurs.

## Address Function

- Returns the address of a simple server.

## LoadBalancer Methods

- `serveProxy`: Proxies incoming HTTP requests to the next available server obtained from `getNextAvailableServer()`.

## Main Function

- Initializes a list of servers with different addresses (Facebook, Bing, DuckDuckGo).
- Creates a load balancer instance with the specified port and the list of servers.
- Defines a request handler function (`handleRedirect`) to forward incoming requests to the load balancer.
- Starts an HTTP server to listen for incoming requests on the specified port.
- Prints a message indicating that the server is running.

Overall, this project demonstrates a basic implementation of a load balancer in Go, where incoming requests are distributed among multiple backend servers using a round-robin algorithm. The `net/http` package is used for handling HTTP requests and responses, and the `httputil` package is utilized for reverse proxying.
