---
title: "REST: Practical Fundamentals"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 3
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

Here's a takeaway of the abstract ideas we covered on the last page:

- **State**: data that can change (transition) through interactions between an API and its client

- **Representation**: the convertible format that enables state to be transferred and used by the client and API

- **Resource**: the representation of a type of state (as an entity or collection) that the API exposes to its client for interaction

Now that you have an understanding of these concepts, let's turn our attention to the practical details of working with REST APIs. 
The following sections reference the CodingEvents MVC project we've been creating over the last several lessons to illustrate 
the capabilities of an alternative CodingEvents API project.

### Shapes

**Shape** describes the input or output of an API in terms of its fields and data types. There are no rules for how shapes should be defined. However, the goal should be to describe shapes in a way that is easy to understand. For this reason, shapes are typically shown in a way that is similar to the representation format. Because we use JSON as the representation format, the 
[JSON data types](https://json-schema.org/understanding-json-schema/reference/type.html) are used. 

You can think of shape like a class definition in an object-oriented codebase:

{{% notice blue "Example" "rocket" %}}
```csharp {linenos=table}
public class CodingEvent {
    public int Id { get; set; }
    public string Title { get; set; }
    public string Description { get; set; }
    public DateTime Date { get; set; }
}
```
{{% /notice %}}

Notice, the class called ``CodingEvent`` is equivalent to the ``Event`` class in our MVC application.

The output resource shape of a CodingEvent entity:

```bash {linenos=table}
CodingEvent {
    Id: integer
    Title: string
    Description: string
    Date: string (ISO 8601 date format)
}
```

The JSON representation of the resource that the API sends out is then based on the shape. This is like how an object is based on 
the blueprint of its class.

Here's a CodingEvent JSON Representation:

{{% notice blue "Example" "rocket" %}}
```bash {linenos=table}
{
    "Id": 1,
    "Title": "Halloween Hackathon!",
    "Description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
    "Date": "2020-10-31"
}
```
{{% /notice %}}

We can think of inputs as a *partial state* provided by the client during create and update operations. Only some of the fields 
are included because the API is responsible for providing the others.

Consider the following example of an input shape used to create an event. Notice that the ``Id`` field is not included:

{{% notice blue "Example" "rocket" %}}
```bash {linenos=table}
CodingEvent {
    Title: string
    Description: string
    Date: string (ISO 8601 date format)
}
```
{{% /notice %}}

Some of the common fields the API is responsible for managing:

- the unique identifier (``Id``) 
- the "created on" or "last updated" timestamp
- links for relationships between resources

### Endpoints

An API **endpoint** refers to the HTTP path and method that defines the location of a resource and the action to take on its state.

Endpoints are what an API exposes to its consumers. Each endpoint is made up of two components:

- **path**: the noun that identifies the resource
- **method**: the verb, or action, to take on the resource's state

### Identifying the Resource

Paths are used to identify the resource being interacted with. Recall the hierarchal nature of resources where an entity only 
exists within a collection. RESTful APIs separate the resources they expose into one or more resource entry-points.

Let's consider two resources exposed by a RESTful API:

{{% notice blue "Example" "rocket" %}}
The CodingEvents API would have the following familiar resources (among others):

| Resource | Path |
|----------|-------|
| Coding Event | /events |
| Tag | /tags|
{{% /notice %}}

The name of the path is arbitrary but should follow these rules of thumb to maintain consistency:

- is lowercase and separated by underscores if necessary
- adequately describes the resource in as few characters as necessary
- is a plural noun (actions are described by the method of the endpoint)

Let's see this in action with a CodingEvents API. Using what we have learned so far, we can expect the state of the resource 
collection to be represented in a JSON array:

{{% notice blue "Example" "rocket" %}}
Here is a response from a request to the GET `/events` endpoint:

```bash {linenos=table}
[
    CodingEvent { ... },
    ...
]
```
{{% /notice %}}

The state of the ``CodingEvent`` collection is made up of the collective state of each ``CodingEvent`` entity within it.

{{% notice blue "Example" "rocket" %}}
Here is a response from a request to the GET `/tags` endpoint:

```bash {linenos=table}
[
    Tag { ... },
    ...
]
```
{{% /notice %}}

A request to the endpoint of the `Tag` collection would include its respective `Tag` entity representations (JSON objects).

Suppose we wanted to interact with an individual resource entity. We would need to identify it within its collection. 

The path to identify a resource entity would need to include:

- the collection identifier, or resource entry-point (`/collection`)
- the unique resource entity identifier (`/{entityId}`) within the collection

Because the unique identifier of the entity is variable, we use a path variable (`{entityId}`) to describe it in a generic way.

{{% notice green "Tip" "rocket" %}}
The hierarchy of collections and entities is similar to directories and files. To identify an entity is like identifying a 
file within a directory. You need both the directory (collection) name and a sub-path that uniquely identifies the file (entity).
{{% /notice %}}

{{% notice blue "Example" "rocket" %}}
The generic path to identify a `CodingEvent` resource is noted as `/events/{codingEventId}`.

Let's assume a CodingEvent entity exists with an `Id` of `12`.

We could make a request to the `GET /events/12` endpoint to read its current state and receive this response:

```bash {linenos=table}
{
    "Id": 12,
    "Title": "Halloween Hackathon!",
    "Description": "A gathering of nerdy ghouls...",
    "Date": "2020-10-31"
}
```
{{% /notice %}}

### CRUD Operations & HTTP Methods

As we saw in the previous article, state is something that can be interacted with using CRUD operations. By convention, each of these 
operations corresponds to an HTTP method:

| HTTP Method | CRUD Operation |
|-----|-----|
| `POST` | `Create`|
| `GET`| `Read`|
| `PUT/PATCH` | `Update` | 
| `DELETE` | `Delete` |

The use case of an API dictates the design of its contract. This includes which actions the client can take on each resource. In 
other words, not every action must be exposed for each resource the API manages.

{{% notice blue "Note" "rocket" %}}
If a client tries to take an action on a resource that is not supported by the API, they will receive a ``405`` status code or 
``Method not allowed`` error response.
{{% /notice %}}

### Endpoint Behavior

Depending on the endpoint, the effect of a request can differ. In other words, the behavior of an endpoint is dependent on the subject -- an entity or the collection as a whole.

### Operating On Collections

| HTTP Method | Behavior with resource state |
|-----|-----|
| `POST` | `create a new entity in the collection`|
| `GET`| `view the current list of all entities in the collection`|
| `PUT/PATCH` | `bulk update of entities in the collection` | 
| `DELETE` | `remove all entities in the collection` |

{{% notice blue "Note" "rocket" %}}
Exposing the ability to modify or delete all of the entities in a collection at once can be risky. In many cases, the design of a RESTful API will only support `GET` and `POST` endpoints for collections. 
{{% /notice %}}

Let's consider a request for creating a resource entity. Recall that this operation acts on the state of the collection by 
adding a new entity to it.

{{% notice blue "Example" "rocket" %}}
As we saw earlier, the input shape for creating an event only includes the fields the consumer is responsible for. The ``Id`` 
field is then managed internally by the API.

We refer to this shape as a ``NewCodingEvent`` to distinguish it from the ``CodingEvent`` resource shape:

```bash {linenos=table}
NewCodingEvent {
    Title: string
    Description: string
    Date: string (ISO 8601 date format)
}
```

We can describe this request in a shorthand: 

`POST /events (NewCodingEvent) -> 201, CodingEvent`

This shorthand includes:

1. The endpoint method: `POST`
1. The endpoint path: `/events`
1. The name of the request body: `(NewCodingEvent)`
1. The returned status code: `201`
1. The returned response body: `CodingEvent`

After sending this request, the response includes:

- a `201`, or `Created`, status code
- a `Location` response header
- the representation of the created resource entity state (including an assigned `Id` field)
{{% /notice %}}

### Operating On Entities

| HTTP Method | Behavior with resource state |
|-----|-----|
| `POST` | N/A (created inside a collection)|
| `GET`| view the current entity state |
| `PUT/PATCH` | update the entity state | 
| `DELETE` | remove the entity from the collection |

When removing a resource, the client is requesting a transition to an empty state. This means that both the request body and response body that are transferred (the representations of state) are empty. We can see this behavior in action with a request to the ``DELETE`` endpoint for a single resource entity in our example API:

{{% notice blue "Example" "rocket" %}}
Let's once again assume a `CodingEvent` resource exists with an `Id` of `12`. If we want to remove this entity, we need to issue a request to its uniquely identified `DELETE` endpoint:

`DELETE /events/12 -> 204`

In this shorthand, you can see that this request has an empty request body. This is the empty state we are requesting a transition to. 
The `204`, or `No Content`, status code in the response indicates that the action was successful and that the response body is empty. The API transfers back a representation of empty state (no response body) to the client.
{{% /notice %}} 

{{% notice blue "Example" "rocket" %}}
What would happen if we made another request to the endpoint of a resource entity that doesn't exist, `DELETE /events/999`?

We would receive a`404`, or `Not Found`, status code that lets us know the request failed because of a client error (providing an `Id` for a nonexistent resource).
{{% /notice %}}

### Headers & Status Codes

A RESTful API uses HTTP response status codes and HTTP request and response headers. Response status codes inform 
the client if their request is handled successfully or if changes are needed to fix a request. 

HTTP headers are used to communicate additional information (metadata) about a request or response. Let's take a look at the status codes now.

#### Status Codes

Every RESTful API response includes a status code that indicates whether the client's request has succeeded or failed.

#### Success Status Codes

When a request is successful, the `2XX` status codes are used. These codes communicate to the consumer the type of success relative to the action that was taken. Below is a list of the common success codes you will encounter:

**Common client success status codes for each action:**

| HTTP Method | Status Code | Message | Response |
|-----|-----|-----|-----|
| `POST` | `201` | `Created` | Resource entity and `location` header |
| `GET`| `200` | `OK` | Resource entity or collection |
| `DELETE` | `204` | `No Content` | empty response body |

.. list-table:: Common client success status codes for each action
   :header-rows: 1
   :widths: 20 20 20 40

#### Failure Status Codes

Requests can fail. Status code groups categorize two types of failure:

- **client error**: `4XX` status code group
- **server error**: `5XX` status code group

Client errors indicate that a request can be reissued with corrections. Each of these 
status codes and messages notify the consumer of the changes needed for a success. In contrast, server errors cannot be remedied by the client sending the request. 

Let's look at some of the common client error status codes:

| Status Code | Message | Correction |
|-----|-----|-----|
| `400` | `Bad Request` | Client must fix errors in their request body |
| `401`| `Unauthorized` | Client must authenticate first |
| `403` | `Forbidden` | An Authenticated client in not allowed to perform the requested action |
| `404` | `Not Found` | The path to identify the resource is incorrect or the resource does not exist |


A bad request will include an error message in its response. The message should indicate what the client must change in their request body to succeed. This failure is seen when creating or updating a resource entity:

{{% notice blue "Example" "rocket" %}}
In the CodingEvents API, the state of a `CodingEvent` is validated using the following criteria:

- `Title`: 10-100 characters
- `Description`: less than 1000 characters

Imagine a client sending a `PATCH` request to update the `CodingEvents` resource entity with an `Id` of `6`. 

`PATCH /events/6 (PartialCodingEvent) -> CodingEvent`

If their request body contains a `Title` field that is too short, the request will receive a `400` status code:

Here is a portion of an invalid request to the `PATCH /events/6` endpoint:

```bash {linenos=table}
{
    "Title": "Foo"
}
```

`Foo` does not contain enough characters to be a valid CodingEvent title. The CodingEvents API response to such a request therefore includes a `400` status code. 
This alerts the client that they must correct their data representation. The response body indicates which aspects of the request are invalid. This is a 400 failed response body:

```bash {linenos=table}
{
    "error": "invalid fields",
    "fields": [
    {
        "Title": "must be between 10 and 100 characters in length"
    }
    ]
}
```

Using the information in the response, the client can fix their request body and reissue the request successfully.
{{% /notice %}}

{{% notice blue "Note" "rocket" %}}
The `401`, or `Unauthorized`, status code actually indicates that the consumer is not authenticated. This means the consumer has not proven their identity to the API. The `403`, or `Forbidden`, status code is a more accurate description of being unauthorized. After authenticating, the consumer's authorization can determine if they are allowed or forbidden from taking the requested action.
{{% /notice %}}

#### Headers

In RESTful design, HTTP headers communicate metadata about each interaction with a resource.

**Common request/response headers in REST:**

| Request/Response | Header | Meaning | Example |
|-----|-----|-----|-----|
| Both | `Content-Type` | The attached body has the following media type | `application/json` |
| Request | `Accept` | The client expects the requested resource representation in the given media type | `application/json` |
| Response | `Location` | The created resource representation can be found at the given URL value | `/resources/{id}` |

{{% notice green "Tip" "rocket" %}}
The `Authorization` request header is also commonly used. 
{{% /notice %}}

### Learning More

These articles have covered the fundamental aspects of the RESTful mental model and practical usage. However, RESTful design is a deep topic that even 
extends beyond the web and use of HTTP! 

If you want to learn more, the following links are a good start:

#### Practical Understanding

- [Craig Dennis: APIs for beginners (YouTube)](https://www.youtube.com/watch?v=GZvSYJDk-us&t=0s)
- [REST sub-collections, relationships and links](https://restful-api-design.readthedocs.io/en/latest/relationships.html)
- [OpenAPI specification & Swagger REST tools](https://swagger.io/specification/)
- [The GitHub API](https://developer.github.com/v3/) and [Stripe (payment processing) API](https://stripe.com/docs/api) are excellent examples of RESTful design (and fantastic documentation)

#### Deep Understanding

- [the REST constraints](https://www.restapitutorial.com/lessons/whatisrest.html)
- [The Richardson REST maturity model](https://www.martinfowler.com/articles/richardsonMaturityModel.html)
- [the original REST doctoral thesis by Roy Fielding](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)

### Check Your Understanding

{{% notice green "Question" "rocket" %}}
A `POST` request performs which type of action?

`a.` Create

`b.` Read

`c.` Update

`d.` Delete
{{% /notice %}}

{{% expand "Check your solution" %}}
`a:` Create
{{% /expand %}}

{{% notice green "Question" "rocket" %}}
The _________ portion of a RESTful URL identifies the resource.

`a.` path

`b.` query

`c.` host

`d.` user
{{% /notice %}}

{{% expand "Check your solution" %}}
`a:` path
{{% /expand %}}

