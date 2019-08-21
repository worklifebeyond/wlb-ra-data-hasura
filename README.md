# ra-data-hasura

> [react-admin](https://github.com/marmelab/react-admin) data provider for Hasura GraphQL Engine. Forked from [Hasura GraphQL Engine](https://github.com/hasura/graphql-engine/tree/master/community/tools/ra-data-hasura) and customized for internal usage.


## Motivation

### why this

Since `Hasura GraphQL Engine` has monorepo for all core engine and even community tools, we forked as a single repository for simplicity and focused on what we need without messing up with another stuff that not related with our need. 

### Customization

Hasura access control is [role based](https://docs.hasura.io/1.0/graphql/manual/auth/authorization/common-roles-auth-examples.html). Let say we have role `admin-platform`; can fetching `all users` with results like `id` `email` `name` `biography`, but can only update `biography`.

In the other side, [React Admin](https://github.com/marmelab/react-admin) by design is performed `update` with `parameters` that we've fetched before. 
So, instead of `update` only `biography` field, it actually updates whole fields even though has no changes in the data.
See [this issue](https://github.com/marmelab/react-admin/issues/2414#issuecomment-428945402) for details. 

To achieve this if you want to send only the values that changes to your `hasura engine`, you need to compute the diff in the `dataProvider` and send only this diff.
