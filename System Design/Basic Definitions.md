

# Basic definitions of entities involved in system design 


### Gateway / Proxy server

In a microservice architecture, gateway is an additional layer positioned in front of all microservices, handling some responsibilities as follows:

 - Routing requests to the appropriate microservice. Like lets say gmail.com/auth. Upon seeing /auth, the gateway routed requests to the auth service 
 - Block or blacklist requests which have a malicious intent, like having ratelimiter functinality inside to handle load balancing and DDOS attacks
 - Translating HTTP requests, like into TCP.

Sometimes, we can decouple the responsibility of route to service mapping using an additional layer called "Service Manager", to avoid too many responsibilities for Gateway. All services register themselves with the Service manager that hey, Im responsible for this, send me certain kind of requests. Gateway asks service manager to give details about where to route a request, and send it accordingly <br/>


### API contracts and versioning

In the context of GMAIL app, lets say a Profile service registered itself with the Gateway. Then gateway routes requests to the Auth service, by creating a JSON object and making a call to the service API.<br/>

Here, how does gateway know how to create the appropriate object which can be used properly by Auth service. The Auth service sends info about how it needs the object to its call. It uses a service registry, and in there it puts its specifications (something like SWAGGER), so that other users refer to that service registry when communicating with the service.<br/>

<b>A service registry is a database for the storage of data structures for application-level communication. It serves as a central location where app developers can register and find the schemas used for particular apps</b>

The service registry definitions keep changing, so we version them something like v3, or v4. So in here, lets say gateway has version v4 registered for Auth service, it mentions that in its call. And Auth service handles the request according to the version of service registry definition the Gateway used to

### Things to reserach

 - Reverse Indexing 
 - Lucene (Search Engine in Emails service)



