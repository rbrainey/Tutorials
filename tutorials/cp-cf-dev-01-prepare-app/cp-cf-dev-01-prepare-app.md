---
parser: v2
auto_validation: true
primary_tag: software-product>sap-business-technology-platform
tags: [  tutorial>beginner, software-product>sap-business-technology-platform, programming-tool>node-js ]
time: 10
---


# Download and Prepare App for Cloud Foundry Deployment
<!-- description --> Download files for a simple app, maintain the deployment descriptor, and bundle everything together ready for deployment.

## You will learn
- What a typical small Node.js app looks like
- What a Cloud Foundry deployment descriptor contains

## Intro
In this tutorial, you'll download a simple Node.js app from GitHub that returns an index page with various information about itself, in response to an HTTP request. You'll open up and edit the app's deployment descriptor, a file containing information about the app, including memory requirements, hostname and more.

---

### Find the sample app on GitHub


The sample app is available in a repository on GitHub.

Open it up at this URL: <https://github.com/SAP-samples/cf-sample-app-nodejs>.


### Download sample files


This tutorial is preparing the app for deployment to the SAP BTP, Cloud Foundry runtime, and you'll be deploying it (in another tutorial) from your own machine. So you'll need to download the repository first.

Choose **Clone or download** and then choose **Download ZIP**.

![Download sample files](download-zip.png)

Enter the name of the file you just downloaded and choose **Validate**.




### Extract sample files


Open the zip file and extract its content to a folder on your local computer. You will have extracted a folder named `cf-sample-app-nodejs-main`.



### Open the deployment descriptor


The sample app repository contains a basic deployment descriptor, but you'll need to edit it before the deployment. The deployment descriptor is the file called `manifest.yml` in the root of the app folder structure.

Open the `manifest.yml` file with an editor of your choice.

What is the value of the `name` parameter that exists already in the `manifest.yml`?



### Ensure your application is available via a unique URL

The host name for your app must be unique within a combination of region and runtime, in that it forms the most significant part of the fully qualified hostname in the app's URL space. For example, if your app host name is `myapp`, the fully qualified hostname for the Cloud Foundry runtime in the `EU10` region will be:

`myapp.cfapps.eu10.hana.ondemand.com`

If someone else is already using that hostname within that region and runtime, you won't be able to deploy your application. As this is just a sample application, you can use the `random-route` manifest attribute to have a unique route URL generated for you.

Change the value for `random-route` from `false` to `true` in the `manifest.yml` file:

```yaml
---
applications:
- name: cf-nodejs
  memory: 192M
  instances: 1
  random-route: true
```

To finish off, take a look at the [App manifest attribute reference](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest-attributes.html) to find out more about what you can specify, and, perhaps more importantly, what you [cannot specify any more](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest-attributes.html#deprecated).

---
