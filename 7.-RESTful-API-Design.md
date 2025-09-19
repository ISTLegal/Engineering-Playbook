# RESTful API Design

A comprehensive guide for designing RESTful APIs that are intuitive, maintainable, and developer-friendly.

## 🎯 Purpose

RESTful API design serves as the foundation of modern web services by:

- **Developer Experience**: Intuitive and easy-to-use APIs
- **Scalability**: APIs that grow with your business needs
- **Maintainability**: Well-structured and documented APIs
- **Interoperability**: Standards-based communication
- **Performance**: Efficient data exchange
- **Security**: Secure and authenticated access

## 📋 API Design Fundamentals

### Core Principles

**REST (Representational State Transfer)**:

- **Stateless**: Each request contains all necessary information
- **Client-Server**: Separation of concerns between client and server
- **Cacheable**: Responses can be cached for performance
- **Uniform Interface**: Consistent interaction patterns
- **Layered System**: Hierarchical system architecture
- **Code on Demand**: Optional server-side code execution

### Design Characteristics

**Easy to Read and Work With**:

- **Intuitive URLs**: Clear, descriptive resource paths
- **Consistent Naming**: Standardized naming conventions
- **Clear Documentation**: Comprehensive API documentation
- **Predictable Patterns**: Consistent request/response formats

**Hard to Misuse**:

- **Validation**: Strong input validation and error handling
- **Error Messages**: Clear, actionable error responses
- **Rate Limiting**: Protection against abuse
- **Authentication**: Secure access control

**Complete and Concise**:

- **Full CRUD Operations**: Complete resource lifecycle support
- **Comprehensive Coverage**: All necessary endpoints
- **Efficient Responses**: Only necessary data in responses
- **Versioning**: Backward compatibility support

### Design Flow

The Design Guide suggests taking the following steps when designing resource-oriented APIs (more details are covered in specific sections below):

- Determine what types of resources an API provides.
- Determine the relationships between resources.
- Decide the resource name schemes based on types and relationships.
- Decide the resource schemas.
- Attach a minimum set of methods to resources.

### Resources

Resources are fundamental to the concept of REST. A resource is an object that’s important enough to be referenced in itself. A resource has data, relationships to other resources, and methods that operate against it to allow for accessing and manipulating the associated information. A group of resources is called a collection.

- A collection contains a list of resources of **the same type**. For example, a user has a collection of contacts.
- A resource has some state and zero or more sub-resources. Each sub-resource can be either a simple resource or a collection resource.

For example, a project management API has a collection of users, each user has a collection of tasks, a project resource, a team resource, and several others.

### Methods

All resources have a set of methods that can be operated against them to work with the data being exposed by the API.

RESTful APIs comprise majorly of HTTP methods that have well-defined and unique actions against any resource. Here’s a list of commonly used HTTP methods that define the CRUD operations for any resource or collection in a RESTful API.

| Standard Method | HTTP Method                   | Description                                      |
| --------------- | ----------------------------- | ------------------------------------------------ |
| List            | GET < collection url >        | Used to retrieve a representation of collection. |
| Get             | GET < resource url >          | Used to retrieve a representation of a resource. |
| Create          | POST < collection url >       | Used to create new resources and sub-resources.  |
| Update          | PUT or PATCH < resource url > | Used to update existing resources.               |
| Delete          | DELETE < resource url >       | Used to delete existing resources.               |

## Requests

**Field name casing convention**

You can follow any casing convention, but make sure it is consistent across the application.

**Searching, sorting, filtering, and pagination**

All of these actions are simply the query on one dataset. There will be no new set of APIs to handle these actions. We need to append the query parameters with the GET method API. Let’s understand with a few examples how to implement these actions.

- **Sorting**: In case, the client wants to get the sorted list of users, the `GET /users` endpoint should accept multiple sort params in the query. E.g `GET /users?sort=name_asc` would sort the users by their name in ascending order.

- **Filtering**: For filtering the dataset, we can pass various options through query parameters.
  E.g `GET /users?status=active&role=developer` would filter the user's list data with the status of active and where the role is developer.

- **Searching**: When searching the user name in users list the API endpoint should be `GET /users?search=John Doe`

- **Pagination**: When the dataset is too large, we divide the data set into smaller chunks, which helps in improving the performance and is easier to handle the response. Eg. `GET /users?page=23&limit=25` means get the list of users on the 23rd page, and limits the list to 25 records.

**Versioning**

When your APIs are being consumed by the world, upgrading the APIs with some breaking changes would also lead to breaking the existing products or services using your APIs.

`http://api.yourservice.com/v1/companies/34/employees` is a good example, which has the version number of the API in the path. If there is any major breaking update, we can name the new set of APIs as v2 or v1.x.x

## Responses

Providing good feedback to developers on how well they are using your API goes a long way in improving adoption and retention. Every client request and server-side response is a message and, in an ideal RESTful ecosystem, these messages must be self-descriptive.

Good feedback involves positive validation of correct implementation and an informative error on incorrect implementation that can help users debug and correct the way they use the API. HTTP status codes are a bunch of standardized codes which has various explanations in various scenarios. The server should always return the right status code.

**2xx (Success category)**

These status codes represent that the requested action was received and successfully processed by the server.

- **200 Ok** The standard HTTP response representing success for GET, PUT or POST.
- **201 Created** This status code should be returned whenever a new instance is created. E.g on creating a new instance, using POST method, should always return a 201 status code.
- **204 No Content** represents the request is successfully processed, but has not returned any content.

**3xx (Redirection Category)**

- **304 Not Modified** indicates that the client has the response already in its cache. And hence there is no need to transfer the same data again.

**4xx (Client Error Category)**

These status codes represent that the client has raised a faulty request.

- **400 Bad Request** indicates that the request by the client was not processed, as the server could not understand what the client is asking for.

- **401 Unauthorized** indicates that the client is not allowed to access resources, and should re-request with the required credentials.

- **403 Forbidden** indicates that the request is valid and the client is authenticated, but the client is not allowed access to the page or resource for any reason. E.g sometimes the authorized client is not allowed to access the directory on the server.

- **404 Not Found** indicates that the requested resource is not available now.

- **410 Gone** indicates that the requested resource is no longer available and has been intentionally moved.

**5xx (Server Error Category)**

- **500 Internal Server Error** indicates that the request is valid, but the server is totally confused and the server is asked to serve some unexpected condition.

- **503 Service Unavailable** indicates that the server is down or unavailable to receive and process the request. Mostly if the server is undergoing maintenance.

## Additional Resources

- [Google's API Design Guide](https://cloud.google.com/apis/design/)
- [Best Practices in API Design](https://swaggerhub.com/blog/api-design/api-design-best-practices/)
- [API Design Guidelines](https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9)
