# Middleware

## Objective

In order to enable a flexible way to support cross cutting features, client libraries should support a pipeline of pluggable middleware.  Users should be able to remove existing middleware, replace it and add new piece of middleware at any location in the pipeline.  

## Requirements

- A Middleware pipeline should be configured so that all requests are passed through the chain of middleware in the same order and responses are processed in reverse order to requests.  
- A default pipeline should be configured by the Graph Client Factory for providing standard Graph behaviour.
- A pipeline can be customized at the time of creation of a HTTP client.  Pipelines should not be reconfigured at runtime.
- Middleware should accept a native or wrapped request object and also process the corresponding response.
- Middleware components should be as cohesive as possible with an effort to minimize dependencies on other pieces of middleware.
- A request context object should be passed along with the request object, to allow the behaviour of middleware to be adjusted based on the specifics of the request and state aggregated by other pieces of middleware.
- The request context object should provide a dictionary of optional middleware control objects that can be accessed by middleware components to allow customized behavior.  

## Performance Considerations

Due to the fact that every request and response pass through each and every piece of middleware it is important that processing is efficient.  Middleware pipelines can be used on both application servers as well as clients so they need to be able to support a high volume of request and be thread safe.

Middleware should be cautious about preserving state between the processing of the request and the handling of the response as this can put significant memory pressure on high load servers.

## Security Considerations


## Example Usages