## Protocols of the Web

For anything on the web, the format which we send and receive data is in HTTP format, the Hypertext Transfer Protocol. It's the agreed-upon shape that requests and responses take so that any client and any server can understand each other.

When you type in a URL in your browser starting with http or https, your browser, the client, is making an http request to a server. The server then responds with the requested resource, which is often a webpage.

![[Screenshot 2026-06-28 at 11.14.08 AM.png|500]]

We don't need to implement HTTP ourselves, we just need to understand the shape of what we're sending and receiving.

There's a request header and request body for every HTML request.

![[Screenshot 2026-06-28 at 11.17.46 AM.png|500]]

And this is it's format:

![[Screenshot 2026-06-28 at 11.47.07 AM.png|500]]

Whenever we send request to a server, it will respond with a status code, An HTTP status code is a three-digit number sent by a web server to a client (like a browser or an API consumer) indicating the specific outcome of a request.

Here are some common ones you'll be seeing:
- 200 OK: success; here's what you asked for.
- 400 Bad Request: your request was malformed; the server couldn't parse it.
- 404 Not Found: valid request, but the thing doesn't exist.
- 500 Internal Server Error: the server's own code broke; not your fault.

In general, these codes could be described in such catergories.
- 1xx- informational
- 2xx- you succeeded
- 3xx- redirect
- 4xx- you did something wrong
- 5xx- server did something wrong

---
## APIs

We've actually been using all sorts of APIs throughout our coding life without realizing, as all that an API is is just a systematic way for our code to call external services, you need to make a request in a specific format, the api will respond in a specific format.

![[Screenshot 2026-06-28 at 10.28.05 AM.png|500]]

I know... looking at API is annoying and trivial, since it's not really like... knowledge? It's just a rule book full of commands of what inputs a function takes, and what outputs will it spit out, yet you have no idea how the API server does it.

```python
from openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-5.5",
    input="Write a short bedtime story about a unicorn."
)

print(response.output_text)
```

For example, this is some API call from OpenAI, where I import this python library by them, and then just have a 'function' that inputs a model, and a piece of text, and I'm suppose to magically accept that it will return the answer in a neat, formatted way.

And then if you dig into it, there's thousands of commands lying in there, completely unrelated and is just like the book of the law for memorization!

Also, the idea won't transfer over to if you are doing API calls from Anthropic, good luck!

```python
import anthropic

client = anthropic.Anthropic()

message = client.messages.create(
  model="claude-opus-4-8",
  max_tokens=1024,
  messages=[{
    "role": "user",
    "content": "Hello, Claude"
  }]
)
print(message.content[0].text)
```


Many External APIs will require you to get an API key or token to either rate limit, or charge you for using their API.
- It's not free lunch ya know... bots run wild on the internet these days


The main benefit of APIs is that the client does not have to worry about what database the server is using or how data is organized in general. 

We never have to worry about querying the database or implementing the logic necessary to organize our data. As a client, we trust that the API does the thing that it says it does and we happily receive the data that we request.

And so, our code is just happy staying within the perimeters of the client, and how it interacts with server!

![[Screenshot 2026-06-28 at 1.17.01 PM.png]]

---
## API With U

So how do we actually use APIs? We've seen them (maybe) a few times in python, but what about react & javascript.

In the browser, JavaScript has a built-in way to make HTTP requests: `fetch()`. It's just a function that takes a URL and returns a Promise.

APIs need to have a 'promise' because API requests might take a while to resolve, and if the API request had to return the result, the client would have to wait however long the API takes
- Promises allow clients to do things while the server takes its time fulfilling the request

Here's the simplest version, hit a public API and log the result:

```javascript
fetch("https://api.github.com/users/9skie")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Something went wrong:", error));
```

Line by line:
- `fetch(url)`: sends a GET request (like typing in your browser bar).
- `.then(response => response.json())`: the response is raw HTTP. `.json()` parses the body into a usable JS object.
- `.then(data => ...)`: you've got your data. Access whatever the API returned.
- `.catch(error => ...)`: network errors or bad URLs end up here.

Same thing reads more like normal code with `async/await`:

```javascript
async function getUser() {
  const response = await fetch("https://api.github.com/users/9skie");
  const data = await response.json();
  console.log(data);
}
```

`await` pauses until the data comes back. `async` lets you use `await`.

That's the whole pattern for any REST API: fetch a URL, parse JSON, use the data. Only the URL and the response shape change.

