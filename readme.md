# Echo Plugin

Echo Plugin is a middleware for [Traefik](https://github.com/traefik/traefik) that shortcuts the response and echoes basic request params in JSON response (path, IPAddress)

## Configuration

## Static

```toml
[pilot]
    token="xxx"

[experimental.plugins.echo]
    modulename = "github.com/traefik/plugin-echo"
    version = "v0.1.0"
```

## Dynamic

To configure the `Echo` plugin you should create a [middleware](https://docs.traefik.io/middlewares/overview/) in 
your dynamic configuration as explained [here](https://docs.traefik.io/middlewares/overview/). The following example illustates
the usage of `echo` middleware plugin on specific path (`/echo`). 

```toml
[http.routers]
  [http.routers.my-router]
    rule = "Path(`/echo`)"
    middlewares = ["echo"]
    service = "my-service"

[http.middlewares]
  [http.middlewares.echo.plugin]
    include-host = true
[http.services]
  [http.services.my-service]
    [http.services.my-service.loadBalancer]
```