# Evolve APIs 

This Project is a forked from nfrankel/evolve-apis. 
Official documentation can be found [here](https://apisix.apache.org/docs/).
Other interesting examples and use cases with code to try it your self can be found [here](https://apisix.apache.org/docs/general/code-samples/). 

It is a short and small demonstration of Apisix. The use case is to evolve an API from version 1 to version 2. 

## Overview of the System Ports

| System              | Port | Function                                          |
|---------------------|------|---------------------------------------------------|
| APISIX - Config API | 9180 | Configure the API gateway via HTTP requests.      |
| APISIX - Dashboard  | 9000 | Configure the gateway via UI and see a dashboard. |
| APISIX              | 9080 | The API of the Gateway                            |
| Old-API             | 8081 |                                                   |
| New-Api             | 8082 |                                                   |
| Prometheus          | 9090 | Time series database to capture events.           |
| Grafana             | 3000 | Dashboard to visualize events.                    |

## How to use this
If you use Linux or macOS you can configure the gateway with the scripts in the evolve directory. 
Because of issues with windows there is also a file to use insomnia. Just import this file and run the requests. 

## Plugins
APISIX works with plugins for many use cases. In this example we use prometheus for monitoring the routes in script 3. 
Later on we use a 'proxy-rewrite' Plugin to rewrite the URI. This is needed because we get a request on v1/hello, this will
be redirected to our backend, the old-api. But the old-api doesn't know a path v1/hello, it just knows /hello. So a regex 
is needed to clear the URI before sending the request to the backend. 

```json
{
  "proxy-rewrite": {
    "_meta": {
      "priority": 1020
    }
  }
}
```
In the example above the priority. This is needed because the priority in APISIX is by default hard coded. 
But can be changed like this.