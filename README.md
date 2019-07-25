# CharityBase Router

There are multiple CharityBase services: a GraphQL API, a legacy REST API, an auth API, a web app and a docs site.  It's tempting to combine all these codebases into a monorepo, however we opt to keep them separate and deploy each to a unique domain.  This router makes use of Now's routing to unify all services under the single domain `charitybase.uk`.  Note that this is _not_ the only entry point - the service-specific domains are still publicly accessible.


```
 +-------+             +--------
 |Web App+---+     +---+Docs v4|-[Deprecated]
 +-------+   |     |   +-------+
             |     |
      +------+-----+-----+
      |CharityBase Router|
      +-----+---+---+----+
            |   |   |
+--------+  |   |   |  +-----------+
|Auth API+--+   |   +--+REST API v4|-[Deprecated]
+--------+      |      +-----------+
          +-----+-----+
          |GraphQL API|
          +-----------+
```

## Requirements

[Now](https://zeit.co/now) - can be installed globally with npm: `npm i -g now`

You either need to use Now's nameservers or create a `CNAME` / `ALIAS` DNS record with value `alias.zeit.co.`


## Creating the Router

From this directory, run:

```bash
now && now alias
```

This only needs to be done once, or anytime the routes to services change.


## Redirect

We could add `www.charitybase.uk` as an alias in the config, however we opt to serve from the naked domain `charitybase.uk` only.  We therefore need to redirect `www` requests to the naked domain.  This can be tricky to achieve with DNS records so we use a separate Now alias to do the redirect.

From the [redirect](./redirect) directory, run:

```bash
now && now alias
```

This only needs to be done once.
