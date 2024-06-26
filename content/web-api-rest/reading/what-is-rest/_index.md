---
title: "What is REST"
date: 2022-12-15T09:16:07-06:00
draft: false
weight: 2
originalAuthor: John Woolbright # to be set by page creator
originalAuthorGitHub: jwoolbright23 # to be set by page creator
reviewer: Kimberly Horan # to be set by the page reviewer
reviewerGitHub: codinglikeagirl42 # to be set by the page reviewer
lastEditor: # update any time edits are made after review
lastEditorGitHub: # update any time edits are made after review
lastMod: 12/15/22 # UPDATE ANY TIME CHANGES ARE MADE
---

**REST** is an acronym that stands for **REpresentational State Transfer**. **RESTful web services** refer to web technologies that use
this design pattern. REST, as we've mentioned, is an architectural pattern that provides uniformity and predictability to any API 
that adheres to it. 

The same benefits are experienced by the API consumer. REST is a set of guiding principles for supporting 
the organization of an API's core responsibilities -- managing and transferring data. The REST pattern organizes the external 
interface, or contract, and does not concern itself with the internal implementation of the API.

Adopting the REST specification into the design of an API provides consistency during development and consumption. Much like 
following the patterns of MVC allows other developers to easily understand your code, following REST patterns gives other developers 
the benefit of understanding how your API is structured and behaves. As an added bonus, a REST API also gives the client application 
a base-line understanding on how to interact with your API.

{{% notice green "Tip" "rocket" %}}
The topics of state and representation are *purposefully abstract* in REST so that they can be applied to any API. Don't get overwhelmed!
{{% /notice %}}
   
### What is State?

State is transitional application data that can be viewed or changed by external interaction. Though state is abstract, programmers interact with it using CRUD operations. 

Imagine viewing, or reading, the state of an application's data as it transitions through each of the following interactions:

1. **Before creating**: Empty state
2. **After creating**: Initial state
3. **After updating**: New state
4. **After deleting**: Empty state

You can see that the state is defined by how the data exists after its latest interaction. 

{{% notice blue "Note" "rocket" %}}
The concept of state is both the most abstract and most fundamental aspect of REST. 
{{% /notice %}}

### What is a Representation?

Representation refers to a depiction of state that is usable in a given context. In the REST context, state must be 
represented in a way that is portable and compatible with both the client and API. 

JSON is a data format that provides structure, portability and compatibility. For these reasons, JSON is the standard representation used when transferring state between a client application and an API. 

{{% notice blue "Example" "rocket" %}}
The state of a *single* `CodingEvent` entity is represented as a single JSON object:

```json {linenos=table}
{
    "Id": 1,
    "Title": "Halloween Hackathon!",
    "Description": "A gathering of nerdy ghouls...",
    "Date": "2020-10-31"
}
```

Whereas the state of a collection of `CodingEvents` is represented by a JSON array of objects.

```json {linenos=table}
[
    {
    "Id": 1,
    "Title": "Halloween Hackathon!",
    "Description": "A gathering of nerdy ghouls...",
    "Date": "2020-10-31"
    },
    ...
]
```

Notice that the state here is represented as the collective state of all of the `CodingEvents` in the collection.
{{% /notice %}}

{{% notice green "Tip" "rocket" %}}
The process of converting an object representation to a JSON representation is called **JSON serialization**.

The inverse process, where JSON is parsed, or converted back to object representation, is called **JSON deserialization**.
{{% /notice %}}

### Transferring a Representation of State

In REST, state is transitioned by interactions between a client and an API. Each transition is driven by transferring a JSON object or collection. A RESTful API is designed to be stateless. 

This has the following implications:

- The state of data is maintained by the client application and the database that are on either side of the interface. 
- State transitions are signals containing data representations, driven by the client and facilitated by the API.

In order to maintain portability between different client and API contexts, we transfer representations of state. These representations can then be converted between the *portable representation* (JSON) and the representation that fits a given context (a JavaScript or C# object). Remember, state is defined by an application's latest CRUD operation. Because every interaction is initiated by the client, we consider the client to be in control of state.

What this means is that the client can:

- Read: request the current representation of state
- Create & Update: transition to a new state by sending a new representation
- Delete: transition to an empty state by requesting its removal

However, it is up to the API to define the contract, or expose:

- the types of state, or resources, the client can interact with
- which (CRUD) interactions are supported for each resource 

These decisions are what drive the design of the contract. 
   
### Resources

While state is an abstract concept, a resource is something more tangible. Simply put, a **resource** is a type of object that an API allows 
client applications to interact with. Resources are categorized as an individual entity or a collection.

**Entity**: a single resource that is uniquely identifiable in a collection.

**Collection**: entities of the same resource type treated as a whole.

We refer to the state of a resource in terms of a single entity or the shared state of a collection.

{{% notice blue "Note" "rocket" %}}
Initially, a collection's state is just empty. If you were to read the collection's state, it would be represented as an empty JSON array, `[]`.
{{% /notice %}}
   
In RESTful design, an individual entity only exists as a part of a collection. A change to the state of an entity inherently changes the state of the collection it is a part of.

When creating an entity, you are operating on the state of the collection that holds it. In order to create it, you must know what collection the entity belongs to.

When reading, updating or deleting an entity, you are directly operating on the state of the entity and indirectly on the state of its collection.

In order to fulfill these operations, you need to know:

- what collection the entity belongs to
- how to uniquely identify the entity within the collection

This hierarchal relationship between collections and the entities within them is an integral aspect of RESTful design. The contract of a RESTful API 
defines the shape, or structure, of its resources along with the hierarchal organization of the endpoints used for interacting with them.

### Check Your Understanding

{{% notice green "Question" "rocket" %}}
True or False: Using HTTP requests, we can perform all four CRUD operations.

1. True

1. False
{{% /notice %}}

<!-- {{% expand "Check your solution" %}}
`a.` True! REST API design relies on HTTP request types to perform CRUD operations on application data
{{% /expand %}} -->

{{% notice green "Question" "rocket" %}}
Reshaping data from object representation to JSON representation is called:

1. JSON parsing

1. JSON reshaping 

1. JSON reserialization

1. JSON serialization
{{% /notice %}}

<!-- {{% expand "Check your solution" %}}
`d.` JSON serialization
{{% /expand %}} -->

