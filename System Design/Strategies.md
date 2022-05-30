
## Basic strategies to keep in mind

 - Don't come up with a huge list of services/features. Or, don't dive too deep into a single service functionality. You will run out of time. Bargain with interviewer that you will speak about only these features for time being or only these functionalities for the time being.
 - When authenticating requests after user logged in, don't always use userID and password. Instead use a JWT token, with an expiry associated with each user (FIP's process in your current work). That token will be added to the cookies and stored in a database table.
 - The service manager info, and the tokens for authentication, are cached in the gateway. Every time these values are updated, they (Service Manager or Auth service) inform gateway to update the cache it has.
 - The cache used above by the gateway is NOT a local cache, but a global cache, which can be accessed by gateway, auth service and other services
 - If you have like a search option in your design, use something like Elastic-Search since the queries would be very slow, operating on more fields and can use just one index. You will store the items or inventory in another DB maybe RDBMS and index/metadata them in Elastic search
