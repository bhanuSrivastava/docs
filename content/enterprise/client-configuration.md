<!--
order: 4
title: Configuring the CLI client
featured: true
-->

# Configuring the CLI client

The client you use to interact with your npm On-Site server is the same client
that you use with the public npm registry.

## Install the latest npm client

npm On-Site requires a 2.x or newer version of the npm client. You can get this
by running:

```
[sudo] npm install npm -g
 ```

<a name="pointing-your-client-to-the-registry"></a>
## Pointing your client to the On-Site registry

Once you have an up-to-date client, you can configure it to install from and
publish to your private npm On-Site registry.

You can do this in one of two ways:

1. [Using On-Site for private _and public_ packages](#using-your-private-registry-for-all-packages)
2. [Using On-Site for private packages only](#using-your-private-registry-for-your-scoped-packages)

Read about each option below.

<a name="using-your-private-registry-for-all-packages"></a>
### Option 1: Using On-Site for private and public packages

If you want all packages, whether they are under a scope or not, to be stored in
your private registry, then you should configure the npm client to use your
private npm On-Site appliance as the top level registry.

To do this, first set your On-Site registry as the CLI's default registry:

```
npm config set registry http://myreg.mycompany.com:8080
```

And then authenticate against your registry without a scope:

```
npm login --registry=http://myreg.mycompany.com:8080
```

When clients are configured this way, they will always use your private npm
On-Site registry as their main registry. When using `npm install`, it will only
look in the private registry to find the package.

To make sure your On-Site instance supports this functionality, you should
enable the "Read Through Cache" setting (enabled by default) in the server's
admin console (`https://myreg.mycompany.com:8800/settings`) so that public
packages are automatically mirrored from the public registry and automatically
added to your registry's whitelist.

<a name="using-your-private-registry-for-your-scoped-packages"></a>
### Option 2: Using On-Site for private packages only

If you want to default to using the public npm registry for most packages and
only use your private registry for packages under a particular scope, then you
can specify that the registry should only be used for that scope.

To do so, use `npm login` with a registry and scope:

```
npm login --registry=http://myreg.mycompany.com:8080 --scope=@myco
```

## Logging in

The `npm login` command will prompt you for your credentials. The credentials
you use should match the authentication strategy configured in the Settings of
your instance's admin console (`https://myreg.mycompany.com:8800/settings`).
**By default, these will be your GitHub or GitHub Enterprise credentials.**

For details on GitHub Enterprise integration, please see
[this page](/enterprise/github).

For details on configuring custom authentication, please see
[this page](/enterprise/custom-authentication).
