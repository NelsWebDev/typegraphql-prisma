---
title: Installation
sidebar_position: 1
---

:::info
Prisma 7 requires **Node.js v20.19.0 or newer**.
:::

### TypeGraphQL

First of all, you should perform all the steps described in the TypeGraphQL installation instruction:

https://typegraphql.com/docs/installation.html

### `typegraphql-prisma` generator

After that, you have to install the generator, as a dev dependency:

```sh
npm i -D typegraphql-prisma
```

Furthermore, `typegraphql-prisma` requires Prisma to work properly, so please install Prisma dependencies if you don't have it already installed:

```sh
npm i -D prisma
npm i @prisma/client
```

Prisma 7's default client requires a driver adapter when you construct
`PrismaClient`. Install the adapter for your database (for example,
`npm i @prisma/adapter-pg pg` for PostgreSQL) and pass it in the `adapter`
option. See the [Prisma driver adapters documentation](https://www.prisma.io/docs/orm/overview/databases/database-drivers).

`typegraphql-prisma` supports Prisma 7. Configure the Prisma Client generator with the
`prisma-client` provider and an explicit output path, as shown in the
[configuration guide](./configuration.md). Prisma 7 also requires database connection
URLs to be configured in `prisma.config.ts`, rather than in the Prisma schema.

### Additional dependencies

You also need to install the GraphQL Scalars library (to support the Prisma `Json`, `BigInt` and `Byte` types):

```sh
npm i graphql-scalars
```

In order to properly support the aggregate and group by queries, the `graphql-fields` package is used, so it also has to be installed:

```sh
npm i graphql-fields @types/graphql-fields
```

Finally, please also install the `tslib` package, which is required for [applying the additional decorators](../advanced/additional-decorators.md) properly:

```sh
npm i tslib
```

### TypeScript configuration

As prisma emits multiple files, make sure you have your tsconfig set properly to `"module": "commonjs"`:

```json {4}
{
  "compilerOptions": {
    "target": "es2021",
    "module": "commonjs",
    "lib": ["es2021"],
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

Otherwise you may experience runtime errors like `ReferenceError: Cannot access 'BankAccountWhereInput' before initialization`.
It's because those generated files rely on each other, so `commonjs` is needed to handle that cyclic imports.
