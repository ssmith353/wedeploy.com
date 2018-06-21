---
title: "Introduction to WeDeploy"
description: "Learn how WeDeploy works in under 5 minutes."
headerTitle: "Getting Started"
layout: "guide"
weight: 1
---

### {$page.title}

###### {$page.description}

<article id="1">

## Why WeDeploy

The goal of WeDeploy is to help developers and companies deploy and ship applications faster. To do this, we take care of all the manual DevOps work for you so you can focus your time and money on building amazing solutions.

We also provide you with intuitive, serverless API's for common application needs like searchable, realtime [databases](/docs/data/), user [authentication](/docs/auth/) and management, and transactional [email](/docs/email/) messaging.

This document walks you through some easy steps to get started on the WeDeploy platform.

</article>

<article id="2">

## Download the CLI

Once you create your [WeDeploy Account](https://console.wedeploy.com/signup), there are two main interfaces by which you can use WeDeploy: the [web Console](https://console.wedeploy.com/) and the [CLI](/docs/configure/command-line/).

To install the CLI on a Unix-like system such as macOS or Linux, open your terminal and run:

```xml
curl https://cdn.wedeploy.com/cli/latest/wedeploy.sh -fsSL | bash
```

<aside>

If you use Windows, check the [Windows amd64 installer](https://bin.equinox.io/c/8WGbGy94JXa/we-stable-windows-amd64.msi). For other systems, see a list of [all builds available](https://dl.equinox.io/wedeploy/we/stable).

</aside>

Then try running `we`. You should be able to see the list of available commands.

**To learn more about what else it can do, check our [CLI Docs](docs/configure/command-line/)**

</article>

<article id="3">

## Deploy a Static Site

Now that you have the CLI installed, you need to login to your account by running `we login` in your terminal.

First, create a directory called `my-app` with a file called `index.html` that contains the following content:

```html
<!DOCTYPE html>
<html>
  <body>
    <p>Hello WeDeploy</p>
  </body>
</html>
```

<aside>

If you are curious about deploying other types of applications like [Node.js](/docs/getting-started/deploying-nodejs/) or [Docker](/docs/getting-started/deploying-docker/), see our [deployment section](/docs/configure/deployment) for more information.

</aside>

Now you can go to the `my-app` directory in your terminal and run this command:

```xml
we deploy
```

Once it deploys, you will see a URL created for your deployment that you can access anywhere. If you redeploy your app, you can see your changes on this URL as well.

</article>

<article id="4">

## Add a Custom Domain

Now that you have a site live, you can add a custom domain to share with others.

Let's try adding prettier domain on your static hosting service for free. Take the `projectID`, or name of your project, that you chose earlier and create a domain from it: `projectID.wedeploy.io`.

To add this alias to your service, all you need to do is run this command:

```xml
we domain
```

It will walk you through a few steps to add your domain.

**To learn more about adding custom domains, check our [Domain and DNS](/docs/configure/domains-and-dns/) docs.**

</article>

## What's next?

Learn more about our [Feature Overview](/docs/getting-started/feature-overview/).