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

<hr />

# useQuery vs useLazyQuery

- `useQuery` executes **automatically** when React component calls, but we can manually call query using `useLazyQuery`.

```js
<Field
  name="category"
  component={FormSelect}
  label="Category"
  options={category_options}
  onChange={(event: any, newVal: string) => {
    getSubCategoryByCategory({
      variables: { categoryId: newVal },
    });
  }}
/>
```

```js
function DelayedQuery() {
  const [getDog, { loading, error, data }] = useLazyQuery(GET_DOG_PHOTO);

  return (
    <div>
      <button onClick={() => getDog({ variables: { breed: "bulldog" } })}>
        Click me!
      </button>
    </div>
  );
}
```

**References:**

- [Manual execution with useLazyQuery](https://www.apollographql.com/docs/react/data/queries/#manual-execution-with-uselazyquery)
- [Apollo Client — How to Query on Click](https://www.apollographql.com/blog/apollo-client/how-to-query-on-click/)

<hr />

# useMutation

**Syntax**

```js
const [login, { data, loading, error }] = useMutation(LOGIN_MUTATION);
```

```js
const [deleteCategory, { data, error, loading }] =
  useMutation<ICategory, IDeleteCategoryVars>(DELETE_CATEGORY, {
    variables: { id: "61d8f06fd76f6d0018ebafa0" },
  });

if (!loading && !error) {
  console.log("Print deleted data: ");
  console.log(data);
}
//JSX
<button
  onClick={() => {
    deleteCategory();
  }}>
  Delete Mutatioin
</button>
```
