---
title: Prisma version verification
sidebar_label: Prisma version check
sidebar_position: 4
---

## Checking installed Prisma version

`typegraphql-prisma` generator works only with selected versions of Prisma.
By default, it checks if the installed Prisma version matches the required one using semver rules.
So when you try to use other version, like a just published, new minor release (or the `dev` one), you will receive an error about wrong package version, e.g:

```sh
Error: Looks like an incorrect version "6.0.0" of the Prisma packages has been installed.
'typegraphql-prisma' works only with selected versions, so please ensure
that you have installed a version of Prisma that meets the requirement: "^7.0.0".
Find out more about that requirement in docs:
https://prisma.typegraphql.com/docs/basics/prisma-version
```

The reason of such restriction is that `typegraphql-prisma` heavily relies on the DMMF and Prisma generators feature which are not considered a public API, so that there's no guarantee about them having no breaking changes in minor releases.
In plenty of previous releases, changes done in Prisma and DMMF impacted `typegraphql-prisma` a lot, so that the generator have produced e.g. invalid classes or even have broken at all.

The current release supports Prisma 7 (`^7.0.0`). Prisma 7's DMMF and generator
interfaces are used by `typegraphql-prisma`, so other major versions are not supported.
The version check is performed by default.

## Lifting Prisma version restriction

If you want to try another Prisma version, you can use `SKIP_PRISMA_VERSION_CHECK`
to suppress that error:

```sh
SKIP_PRISMA_VERSION_CHECK=true npx prisma generate
```

This disables only the version check; it does not make other Prisma versions supported.
