Defines a pattern to match in a URI, as well as a policy or function defining how matching HTTP requests shall be treated.

A rule can be created with three parameters:
- A regex pattern, used to match request URIs
- A redirection URL, where the query will be proxied to
- A rule type, defining how the redirection will happen

### Path matching
When a request URI matches a provided pattern, what comes next in the URI will also be forwarded to the remote host.

For instance, if your Rule is defined as:

```c++
Rule("^/local-path", "https://duckduckgo.com")
```

And you received the following request:

```
GET /local-path?q=Hello%20World HTTP/1.1
```

Then the proxy request will target `https://duckduckgo?q=Hello%20World`.

### Rule types
#### Redirect rules
With redirect rules, the client receives a `302 temporary redirect` responses that sends them towards another URL specified by the rule.

Example:

```c++
const ProxyRequestHandler::Rules ProxyRequestHandler::rules = {
  Rule("^/local-path", "https://duckduckgo.com", Crails::Redirect302)
};
```

#### Proxy rules
Proxy rules are very different: with proxy rules, your Server will actually run the request on its own, before forwarding the remote host response to the client.

Example:

```c++
const ProxyRequestHandler::Rules ProxyRequestHandler::rules = {
  Rule("^/local-path", "https://duckduckgo.com", Crails::Proxy)
};
```

### Advanced rules

For more specific use cases, you can also create a `Rule` with your own [ProxyRequestHandler::RuleSolver], like this:

```c++
const ProxyRequestHandler::Rules ProxyRequestHandler::rules = {
  Rule(
    "^/local-path",
    [](const HttpRequest& request, const std::smatch& matches)
    {
      return ProxyRequest(
        HttpVerb::get,
        "duckduckgo.com",
        443,
        matches.suffix())
          .with_ssl()
    }
  )
};
```

This example reproduces the default behavior for Rules: we reproduce the client request by using whatever came after the detected pattern as the _URI path_.
