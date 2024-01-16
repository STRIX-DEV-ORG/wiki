---
description: Create GraphQL models with Typescript
tags: [typescript, graphql, model, nodejs, javascript]
---

# GUI - Create GraphQL + Typescript models

## Objective

Show an practical and ordered way to create GraphQL + Typescript models.

## Content

### Introduction

You will find several posts, questions with several answers and a variety of solutions you can implement to create GraphQL models when using Typescript, but you will stay wondering which to choose due to the wide differences between them. Based on our investigation we decided to implement a single solution that improves readability, type assertion and isolation of models per file. We are not going to discuss how to instantiate the application or how to serve data with your application by using GraphQL, we are focusing in the models creation only.

### Prerequisites

You need to have a basic understanding of GraphQL and be comfortable with Typescript. You must have a NodeJS server running and your basic project dependencies installed along with the GraphQL core packages for NodeJS.

### Install extra dependencies

There is only one extra dependency that we are going to install for this solution, that is `@graphql-tools/schema`. This package has been developed by an open source API platform called "The Guild" and even when `@graphql-tools` is a heavy package, it has been developed in a module-driven way, giving us the option to install just what we require, in this case, a tool to merge schemas.

Install it by using your prefered node package manager, for example, by using `yarn add @graphql-tools/schema`.

### Folder structure

Given you have your `src` root folder for your code, create a folder called `graphql` inside it, then it will be the parent of a new folder called `types` or `models` (choose the one that makes more sense to you). Finally, create another folder inside `graphql` called `resolvers`.
You will end up having a structure like this:
```text
📁 src
--📁 graphql
----📁 types
----📁 resolvers
--📄 app.ts
```

### The file boilerplate

Inside your `graphql/types` folder, create a new file and call it as your model name, this file will contain your model definitions and will centralize the core graphql functionalitites, every model definition will end-up having the next structure:
```typescript
import { 
    GraphQLSchema,
    GraphQLObjectType, 
    GraphQLNonNull,
    GraphQLInt,
    GraphQLString,
    GraphQLList,
    ...otherTypes,
} from "graphql";

import * as resolvers from '[this-model-resolvers-path]';

export const [YourModel]Type = new GraphQLObjectType({
    // Model attributes deffinitions
});

const [YourModel]Query = new GraphQLObjectType({
    // Model queries deffinitions
});

const [YourModel]Mutation = new GraphQLObjectType({
    // Model mutations deffinitions
});

const [YourModel]Schema = new GraphQLSchema({
    query: [YourModel]Query,
    mutation: [YourModel]Mutation,
});

export default [YourModel]Schema;
```

As you can see, the structure looks simple, clean and understandable, but we are going to break it down for a better understanding.

### Model type definitions

The first and core part of your model will be its definition, here's where you are going to replicate your model's database structure but with GraphQL types, for that, we are going to use RBAC "roles" and "permissions" as example to illustrate what is going on with this definitions:
```typescript title="graphql/types/permission.ts"
// Import the required GraphQL types
import { 
    GraphQLSchema,
    GraphQLObjectType, 
    GraphQLNonNull,
    GraphQLInt,
    GraphQLString,
    // To be used in further configurations
    GraphQLList,
} from "graphql";

// Generate your model definition object
export const PermissionType = new GraphQLObjectType({
    // Give it an internal GraphQL name
    name: 'Permission',
    fields: () => {
        return {
            // Define its attributes
            id: { type: new GraphQLNonNull(GraphQLInt) },
            // GraphQLNonNull is equivalent to "attribute!" in a normal GraphQL schema definition
            name: { type: new GraphQLNonNull(GraphQLString) },
        };
    },
});

/* Further configurations */
```
And of course, we create our role model:
```typescript title="graphql/types/role.ts"
import { 
    GraphQLSchema,
    GraphQLObjectType, 
    GraphQLNonNull,
    GraphQLInt,
    GraphQLString,
    // To be used in further configurations
    GraphQLList,
} from "graphql";

export const RoleType = new GraphQLObjectType({
    name: 'Role',
    fields: () => {
        return {
            id: { type: new GraphQLNonNull(GraphQLInt) },
            name: { type: new GraphQLNonNull(GraphQLString) },
        };
    },
});

/* Further configurations */
```

### Handle relations between models

As you can see, we've created the "role" and "permission" model definitions, but they are not related, thus, our database logic can't be implemented. You might think that a simple import should work to create this relationship, but that will create troubles when working with Typescript, as we might be creating information that would result as undefined under non nullable fields. That's why we will import the related model but once the model using it has been instantiated, thus, avoiding the "undefined" trouble. Also, as we are creating an N to N relationship, we will create another model definition.

```typescript title="graphql/types/rolePermission.ts"
import { 
    GraphQLSchema,
    GraphQLObjectType, 
    GraphQLNonNull,
    GraphQLInt,
    GraphQLList,
} from "graphql";

export const RolePermissionType = new GraphQLObjectType({
    name: 'RolePermission',
    fields: () => {
        // Here we are importing the related models
        const { PermissionType } = require("./permission");
        const { RoleType } = require("./role");

        return {
            id: { type: new GraphQLNonNull(GraphQLInt) },
            // And using those models for the required definitions
            permission_id: { type: new GraphQLNonNull(GraphQLInt) },
            permission: { type: new GraphQLNonNull(PermissionType) },
            role_id: { type: new GraphQLNonNull(GraphQLInt) },
            role: { type: new GraphQLList(RoleType) },
        };
    },
});

/* Further configurations */
```

Role and permission models would need to import the RolePermissionType definition on their own files and use it for the required definitions too, but to keep it simple, we are going to skip that part.

### Model queries

Queries are important when using with GraphQL, as they will dictate how to retrieve information from our models, but we are going to need to create a separate file for each model to do so, the `types` file will handle the definitions and structure and the new file will handle the logic, we are going to place that file under `resolvers`.

```typescript title="graphql/types/role.ts"
/* Previous role type definitions and imports */
const RoleQuery = new GraphQLObjectType({
    // Register this object under an internal GraphQL name, besides your type name
    name: 'RoleQuery',
    fields: () => ({
        role: {
            // What this query will return
            type: RoleType,
            // The params required when reaching this query request
            args: {
                id: { type: new GraphQLNonNull(GraphQLInt) },
            },
            // How to handle the request logic, we will work on this later
            resolve: 'To-Do'
        },
        roles: {
            // This is how you tell that the response will send a list of roles
            type: new GraphQLList(RoleType),
            resolve: 'To-Do'
        }
    })
});
/* Further configurations */
```

### Resolvers

As stated before, resolvers are the ones in charge of the requests logic. Lets create our first resolver, use your model name once again:
```typescript title="graphql/resolvers/role.ts"
// We recommend use CRUD related names for your functions, args is the object defined in your queries
export const readRole: GraphQLFieldResolver<any, any> = async (_parent, args, _context, _info) => {
    // We are obtaining the GraphQLInt that was defined before
    const { id } = args;
    try {
        // As you can see, this example uses prisma, but you might be using mongodb, sequelize or any other tool
        const role = await prisma.role.findUnique({
            where: {
                id,
            },
        });
        return role;
    } catch (error: any) {
        new Error(`Failed to fetch role: ${error.message}`);
    }
};
  
  // Note how it is important the "export" keyword
export const readAllRoles: GraphQLFieldResolver<any, any> = async (_parent, _args, _context, _info) => {
    try {
        const roles = await prisma.role.findMany();
        return roles;
    } catch (error: any) {
        new Error(`Failed to fetch roles: ${error.message}`);
    }
};

/* Mutations functions */
```

Now, go back to your types file and import your resolvers like `import * as resolvers from "[path-to-resolvers]"`. Replace the "To-Do" values with the corresponding resolver, something like `resolvers.readRole`.

### Mutations

Mutations are defined just like the queries, but as GraphQL treats them differently due to how they work with queries being read-only and mutations making modifications to the data, we need to also define them separately.

Make your own definitions and resolver functions, they should result in something like this:

```typescript title="graphql/types/role.ts"
/* Previous role definitions and imports */
const RoleQuery = new GraphQLObjectType({
    // Once more, register this object under an internal GraphQL name
    name: 'RoleMutation',
    fields: () => ({
        createRole: {
            type: RoleType,
            args: {
                name: { type: new GraphQLNonNull(GraphQLString) },
            },
            resolve: resolvers.createNewRole
        },
        updateRole: {
            type: RoleType,
            args: {
                id: { type: new GraphQLNonNull(GraphQLInt) },
                name: { type: new GraphQLNonNull(GraphQLString) },
            },
            resolve: resolvers.updateRole
        },
        deleteRole: {
            type: RoleType,
            args: {
                id: { type: new GraphQLNonNull(GraphQLInt) },
            },
            resolve: resolvers.deleteRole
        },
    })
});
/* Further configurations */
```

### Creating the schema and exporting it

Once you have created your model definitions and resolver functions, you just need to create the final schema definition and export it. That's as simple as:

```typescript title="graphql/types/role.ts"
/* Previous role definitions and imports */
const RoleSchema = new GraphQLSchema({
    query: RoleQuery,
    mutation: RoleMutation,
});

export default RoleSchema;
```

If you have no queries or mutation definitions, don't worry, just don't add them to the schema:

```typescript title="graphql/types/permission.ts"
/* Previous permission definitions and imports */
const PermissionSchema = new GraphQLSchema({
    // We only have a query definitions, but no mutations
    query: PermissionQuery,
});

export default PermissionSchema;
```

### Merge the schemas

GraphQL requires to have all your definitions under a common schema, but as you see, we are going to create a schema per model, resulting in multiple schemas. That's why we installed our dependency that will help us to solve this issue.

First, create an `index.ts` file under your `graphql/types` folder and add the next content to it:

```typescript title="graphql/types/index.ts"
import { mergeSchemas } from "@graphql-tools/schema";

/* Add your model imports */

const schemas = [
    // Add every model schema
];

export default mergeSchemas({ schemas });
```

The `mergeSchemas` function will create a single schema file from all the schemas you provide to it, if you don't give a schema, it won't take it into account and won't appear in your application. Here you have the previous code with the example models we created before:

```typescript title="graphql/types/index.ts"
import { mergeSchemas } from "@graphql-tools/schema";

import RoleSchema from "./role";
import PermissionSchema from "./permission";
import RolePermissionSchema from "./rolePermission";

const schemas = [
    RoleSchema,
    PermissionSchema, 
    RolePermissionSchema,
];

export default mergeSchemas({ schemas });
```

### Using your generated schema

The only thing left is to import your generated schema to be used in your server, you might be using `graphqlHTTP` for that, so here we provide an example on how to do it with it:

```typescript title="app.ts"
/* Your project imports */
// This will import the index.ts from your types folder by default
import graphqlSchema from './graphql/types';

/* Your initial server configurations */

app.use('/graphql', graphqlHTTP({
    graphiql: true,
    schema: graphqlSchema,
}));

/* Further server configurations */
```

### Why JavaScript tag?

Even when we know that all the previous configurations are for Typescript, remember that Typescript is JavaScript with steroids, so all the previous will work with JavaScript. You might only need to remove some Typescript specific assertions.

## Versions

| Version | Description    | Responsibles                     | Date       |
|---------|----------------|----------------------------------|------------|
| 1.0     | Guide creation | Emmanuel Antonio Ramirez Herrera | 09/01/2024 |