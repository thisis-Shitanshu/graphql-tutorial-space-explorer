# Apollo Fullstack Tutorial: Client
- Apollo Client is a complete data management solution for any client.
- It's  intelligent cache, Apollo Client offers a single source of truth for all of the local and remote data in your application.

## Connecting API to CLIENT
- Apollo VSCode uses ENGINE API key to pull down your schema from the registry.
    - apollo.config.js: This config file is how you configure both the Apollo VSCode extension and CLI.

### Fetch Policy:
- Sometimes, it's useful to tell Apollo Client to bypass the cache altogether if you have some data that constantly needs to be refreshed. We can do this by customizing the Query component's  fetchPolicy.
- For Cases: Since we want this list to always reflect the newest data from our graph API, we set the  fetchPolicy for this query to network-only.

## Manage local state
- Store and query local data in the Apollo cache.
- Every app, we display a combination of remote data from our graph API and local data.
    - Apollo Client allows us to store local data inside the Apollo cache and query it alongside our remote data with GraphQL.
- Managing local data:
    - Write a client schema and resolvers for your local data.
    - Query  it with GraphQL just by specifying the @client directive.

1. Write a local schema.
