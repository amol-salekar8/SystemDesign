# API Contract 

An API contract is a document that showcases how an API behaves and how it should be used.

### What Are API Contracts ?
- API contracts can take many forms, such as a document describing the interface, a formal specification written in a particular language, or a set of code examples illustrating how the API should be used
- API Contracts often follow a pre-existing specification like [OpenAPI](https://spec.openapis.org/oas/latest.html), [gRPC](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md), [GraphQL](https://spec.graphql.org/October2021/), [AsyncAPI](https://v2.asyncapi.com/docs/reference/specification/v2.0.0), or [Blueprint](https://apiblueprint.org/documentation/specification.html).
- Using an established standard helps new developers working with your contract learn it faster and it helps your development team save time on creating and maintaining the contract.
- Most standard come with a set of tools and a publicly available community which gives them the advantage of almost always being better than coming up with your own API contract from scratch. These contracts typically set out information such as the API’s expected behavior, data formats, authorization and authentication processes, error handling, and limitations.

### What’s included in an API contract?
- Details about how an application will call the API
- The version or revision of the API technical specification your contract covers
- A commitment to notify the developer of any potential changes in enough time and detail to allow the developer to incorporate the changes in their development cycle
- The format for the data exchange with the application
- Any limitations to the data your contract entitles you to

### How is an API contract utilized?
- **Development.** Serve as a reference point for development guidelines and coding consistency.
- **Access.** Specify who can access the API and how, helping to enhance security.
- **Documentation.** Form the basis for comprehensive API documentation, simplifying adoption.
- **Version management.** Support API evolution while preserving backward compatibility.
- **Automated testing.** Enable reliable testing and validation.
- **Error handling.** Define expected errors and responses, aiding quick issue resolution

### What Should You Consider When Designing an API Contract?
- Keep it simple, easy to understand, and consistent:
  - use a predefined specification to help users learn and integrate your API into their applications
- Document all parts of the API:
  - everyone interacting with your API to have a complete overview of it.
  - The more it is exhaustive, the more they will be able to fully view and understand the structure of your API.
  -  Including elements such as inputs, outputs, error codes, etc. is enormously helpful in the implementation process.
  - Examples are also beneficial as they offer a clear understanding of how the API works and how to incorporate it into applications.
- Thoroughly test the API against the contract:
  - You should test the implementation of your API against the stated contract before release, and provide means of reporting changes - especially breaking ones - or inconsistencies as the API evolves.
  - This means your contract should be in a format allowing your QA process to read and validate against it.

### API Contracts: Best Practices
- Defining the Expected Behavior of the API
- Specifying the Contract and API Version
  - It is common, on an API lifecycle, to see changes to the API behavior itself. As an API grows, changes will be made to the current version of the API.
  - The contract is a good place to communicate to your users and API consumers about the changes in your API and how to keep using your API service after the change applies.
  - If you need to make a breaking change or your API grows and changes so much that you have the need to release a new version of it, you will need to create a new contract.
  ````yaml
      info:
      description: "A simple API example."
      itle: "Example"
      version: "1.2"
    ````
- Document Data Formats, Limitations, and Restrictions

### Reference 
- [https://bump.sh/blog/api-contracts-extended-introduction/](https://bump.sh/blog/api-contracts-extended-introduction/)
- [https://www.adobe.com/acrobat/business/hub/what-s-included-in-an-api-contract.html](https://www.adobe.com/acrobat/business/hub/what-s-included-in-an-api-contract.html)

