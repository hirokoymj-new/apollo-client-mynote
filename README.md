# useQuery

**Syntax**

```js
import { useQuery } from "@apollo/react-hooks";

  const { data, loading } = useQuery<
    ISubCategory,
    ISubCategoryByCategoryVars
  >(SUB_CATEGORY_BY_CATEGORY, {
    variables: {
      categoryId: categoryId,
    },
  });
```

## Options

- query: `DocumentNode`
- variables: { [key: string]: any }

## Fetch policies

By default, the useQuery hook checks the Apollo Client **cache** to see if all the data you requested is already available **locally**. If all data is available locally, useQuery returns that data and doesn't query your GraphQL server. This **cache-first** policy is Apollo Client's default fetch policy.

```js
const { loading, error, data } = useQuery(GET_DOGS, {
  fetchPolicy: "network-only", // Doesn't check cache before making a network request
});
```

- cache-first

  > Apollo Client first executes the query against the cache. This is the default fetch policy.

- cache-only

  > Apollo Client executes the query only against the cache. It never queries your server in this case.

- cache-and-network

  > Apollo Client executes the full query against both the cache and your GraphQL server

- network-only
  > Apollo Client executes the full query against your GraphQL server, without first checking the cache.

**Reference**

- [useQuery](https://www.apollographql.com/docs/react/data/queries/)
- [useQuery options](https://www.apollographql.com/docs/react/api/react/hooks/#options)
- [useQuery - fetch policies](https://www.apollographql.com/docs/react/data/queries/#setting-a-fetch-policy)
