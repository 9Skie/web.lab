In the TLDR sense, A server is something that  processes requests and delivers data to other computers (called "clients") over a network

![[Screenshot 2026-07-01 at 2.18.18 PM.png|500]]

Usually we imagine servers to be some sci-fi place that looks that this:

![[Pasted image 20260701141342.png|400]]

But if we look a bit closer... 

![[Pasted image 20260701141923.png|400]]

Ok, it's just a LOT of storage + some cpus to process incoming & outgoing data traffic.

However, that's not the point of this class, we want to know how us, as web developers interact with servers.

By default, how do requests from us (clients) actually reach a server?


Let's start with an analogy, when you open different applications on a computer, the OS gives each one its own chunk of memory (RAM) to work in.

A server computer has different ports which different processes can each claim one of, so incoming network data gets routed to the right process based on port. 

![[Screenshot 2026-07-01 at 7.27.09 PM.png]]


It's best if we see an example.

By default, all machines have an `IP` . Remote servers, like `github.com`, have a fixed, public IP address, and our personal computers, as we connect to different routers all over the world, have dynamic IP addresses. 

But when we go onto a website, the server and the client must both have an `IP:PORT` in order to talk to each other. We, as clients, send and receive data through a port, and the server sends and receives data through a port as well.

When you are running web development locally, you usually see something like this turn up for your `IP:PORT` , `127.0.0.1:3145`. 

Lets look at the IP first, `127.0.0.1`, this is a special IP that means 'this machine', every computer treats this IP as 'itself', and all requests from our computer client never goes out onto the actual internet.
- `localhost` is just the human-friendly nickname for `127.0.0.1`.

Then lets look at this port, `3145`, this means that somewhere on your machine, a server program is running and told the OS 'port 3145 is for me'.

And so `127.0.0.1:3145` = "on this machine, deliver to whatever process claimed port 3145."

And now, we just saw how we can use our own machine as a server. It just means that our computer will run a program that is designed to actively listen for requests from other computers on a network and respond to those requests.

We are both the sender, and the receiver...

---
## How to Write a Server?

We will use a tool called `node.js` for writing our server, as originally javascript is used for client sided code (it runs on the frontend, and it makes the frontend fancy and interactive and stuff).

![[Screenshot 2026-07-01 at 7.50.33 PM.png|500]]

The backend can be written in other languages as well, like python or java, and there's different tools that help with writing a server for those languages. 

We'll get in touch of this tool much more in practice! But now, back to servers in concept.

---
## Endpoints

What do we do once we actually reach a server? I thought we were suppose to make some requests to it, and it does something, and returns somethings back to us?

