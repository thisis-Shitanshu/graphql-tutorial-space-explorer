# GraphQL Server

## Build Schema
- Schema First Development: schema first before any API development begins.
- Return the data that you're updating in order for the Apollo Client cache to update automatically.

## Hook up your data sources
- An Apollo data source is a class that encapsulates all of the data fetching logic, as well as caching and deduplication, for a particular service.
    - RESTDataSource class: 
        - Responsible for fetching data from a REST API.
        - It also sets up an in-memory cache that caches responses from our REST resources with no additional setup.
            - One can reuse existing caching logic that your REST API exposes.
    - Apollo doesn't have support for a SQL data source yet!

### Creating a datasource:
- You can create your own with the apollo-datasource package.
- Core concepts:
    - The initialize method: You'll need to implement this method if you want to pass in any configuration options to your class.
    - this.context: A graph API's context is an object that's shared among every resolver in a GraphQL request.
    - Caching: While the REST data source comes with its own built in cache, the generic data source does not.

## Writing Resolvers:
- Resolvers are simple and concise because the logic is embedded in the DataSource.
    -  We recommend keeping your resolvers thin as a best practice, which allows you to safely refactor without worrying about breaking your API.
- When writing Query:
    - It's important to give your queries descriptive names so they're discoverable in Apollo developer tooling. 
- You can write resolvers for any types in your schema, not just queries and mutations.

### Authentication
- The Steps:
    1. The context function on your ApolloServer instance is called with the request object each time a GraphQL operation hits your API. Use this request object to read the authorization headers.
    1. Authenticate the user within the context function.
    1. Once the user is authenticated, attach the user to the object returned from the context function. This allows us to read the user's information from within our data sources and resolvers, so we can authorize whether they can access the data.

## Graph in Production:
- An Apollo GraphQL API can be deployed to any cloud service, such as Heroku, AWS Lambda, or Netlify.

### Deploying on Zeit Now, using Apollo Engine account.
1. Publish your schema to Engine:
    - Keep track of schema changes.
    - Apollo Engine contains a schema registry that makes it simple to pull the most recent schema from the cloud.
    - In PRODUCTION set up this publishing script as part of your CI workflow.
1. Get an Engine API key:
    - Create a new Service.
    - Save ENGINE_API_KEY in .env
    - Run:
        ```
        $ npx apollo service:push --endpoint=http://localhost:4000
        ```
1. We will pull down our schema from Engine in order to power the Apollo VSCode extension.
    - For subsequent publishes, we may first want to check for any breaking changes in our new schema against the old version. In a terminal window, run:
        ```
        $ npx apollo service:check --endpoint=http://localhost:4000
        ```