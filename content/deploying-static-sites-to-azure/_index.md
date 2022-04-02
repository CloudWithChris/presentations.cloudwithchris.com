+++
title = "Deploying Static Websites to Azure the cheap and performant way"
outputs = ["Reveal"]
[logo]
src = "images/cwc-logo.png"
[reveal_hugo]
custom_theme = "custom-theme.scss"
custom_theme_compile = true
transition = "none"
+++

{{< slide class="left-align" >}}

# Deploying Static sites to Azure the cheap and performant way

###### Chris Reddington | [@reddobowen](https://twitter.com/reddobowen)

---

{{< slide id="profile" class="left-align" >}}

# Chris Reddington

* Microsoft Cloud Solution Architect
* [Cloud With Chris](https://www.cloudwithchris.com) blogger, podcaster & producer
* [Azure Thames Valley](https://www.meetup.com/Azure-Thames-Valley/)

<br />
 
<div class="container">
  <div class="col">
    <a href="https://www.meetup.com/Azure-Thames-Valley/" style="display: flex; align-items: center; justify-content: center">
      <div>
        <img src="images/Meetup.png" width="50">
      </div>
      <div>
        <p>Azure Thames Valley</p>
      </div>
    </a>
  </div>
  <div class="col">
    <a href="https://github.com/CloudWithChris" style="display: flex; align-items: center; justify-content: center">
      <div>
        <img src="images/GitHub.png" width="50">
      </div>
      <div>
        <p>CloudWithChris</p>
      </div>
    </a>
  </div>
  <div class="col">
    <a href="https://youtube.com/c/CloudWithChris" style="display: flex; align-items: center; justify-content: center">
      <div>
        <img src="images/YouTube.png" width="50">
      </div>
      <div>
        <p>CloudWithChris</p>
      </div>
    </a>
  </div>
</div><div class="container">
  <div class="col">
    <a href="https://twitter.com/reddobowen" style="display: flex; align-items: center; justify-content: center">
      <div>
        <img src="images/Twitter.png" width="50">
      </div>
      <div>
        <p>@reddobowen</p>
      </div>
    </a>
  </div>
  <div class="col">
    <a href="https://github.com/chrisreddington" style="display: flex; align-items: center; justify-content: center">
      <div>
        <img src="images/GitHub.png" width="50">
      </div>
      <div>
        <p>ChrisReddington</p>
      </div>
    </a>
  </div>
  <div class="col">
    <a href="https://linkedin.com/in/chrisreddington" style="display: flex; align-items: center; justify-content: center">
      <div>
        <img src="images/LinkedIn.png" width="50">
      </div>
      <div>
        <p>Chris Reddington</p>
      </div>
    </a>
  </div>
</div>

---

{{< slide class="left-align" >}}

# A quick poll. How is your experience with...

<div class="container">
  <div class="col">
    <ul>
      <li>Hugo, or other Static Site generators?</li>
      <li>
        Azure
        <ul>
          <li>Azure Storage Accounts</li>
          <li>Azure Static Web Apps</li>
          <li>Content Delivery Networks (CDNs)</li>
        </ul>
      </li>
    </ul>
  </div>

  <div class="col">
    <ul>
      <li>Beginner</li>
      <li>Intermediate</li>
      <li>Advanced</li>
    </ul>
  </div>
</div>

---

# This talk will help you...

- Understand the Static Content Hosting Cloud Design Pattern
- Understand the concept of Jamstack and how Static Site Generators like Hugo relate to the above pattern
- Use the relevant Azure Services including Azure Storage or Azure Static Websites, Azure CDN and Azure DNS to implement the pattern

---

{{% section %}}

{{% note %}}
Deploy static content to a cloud-based storage service that can deliver them directly to the client. This can reduce the need for potentially expensive compute instances.
{{% /note %}}

# Static Content Hosting Pattern is useful when...

<div class="container">
  <div class="col">
    <img src="images/static-content-hosting.png" />
  </div>
  <div class="col">
  <ul>
    <li>Wanting to minimise the cost of hosting static resources from expensive compute platforms (e.g. images for a dynamic website, or an entire website that is static in nature)</li>
    <li>Making content accessible across geographical regions by using Content Delivery Networks (CDNs).</li>
  </ul>
  </div>
</div>

---

{{% note %}}
Deploy static content to a cloud-based storage service that can deliver them directly to the client. This can reduce the need for potentially expensive compute instances.
{{% /note %}}

# Static Content Hosting Pattern may not be useful when...

<div class="container">
  <div class="col">
    <img src="images/static-content-hosting.png" />
  </div>
  <div class="col">
  <ul>
    <li>The content is dynamic in nature (e.g. needs to add some additional information before serving the result to client)</li>
    <li>If using this alongside a compute platform and offloading a small amount of static content, is the work/re-architecture worth the reward?</li>
  </ul>
  </div>
</div>

---

# Static Content Hosting Pattern Additional Considerations

<div class="container">
  <div class="col">
  <ul>
    <li>The Static Content must be exposed over an HTTP/HTTPS endpoint so that it can be accessed</li>
    <li>If some content shouldn’t be available anonymously, consider leveraging the Valet Key pattern (e.g. Shared Access Signatures in Storage Accounts)</li>
  </ul>
  </div>
  <div class="col">
    <img src="images/static-content-hosting.png" />
  </div>
</div>

---

# Static Content Hosting Pattern Additional Considerations

<div class="container">
  <div class="col">
  <ul>
    <li>Adopt a CDN to protect the origin and minimise latency (improving performance) for end users</li>
    <li>Consider additional complexity & deployment lifecycle if using this pattern in combination with additional compute platforms</li>
  </ul>
  </div>
  <div class="col">
    <img src="images/static-content-hosting.png" />
  </div>
</div>

{{% /section %}}

---
{{< slide class="left-align" >}}

{{% note %}}
**Pre-rendering**
With Jamstack, the entire front end is prebuilt into highly optimized static pages and assets during a build process. This process of pre-rendering results in sites which can be served directly from a CDN, reducing the cost, complexity and risk, of dynamic servers as critical infrastructure.
With so many popular tools for generating sites, like Gatsby, Hugo, Jekyll, Eleventy, NextJS, and very many more, many web developers are already familiar with the tools needed to become productive Jamstack developers.

**Enhancing with JavaScript**
With the markup and other user interface assets of Jamstack sites served directly from a CDN, they can be delivered very quickly and securely. On this foundation, Jamstack sites can use JavaScript and APIs to talk to backend services, allowing experiences to be enhanced and personalized.

**Supercharging with services**
The thriving API economy has become a significant enabler for Jamstack sites. The ability to leverage domain experts who offer their products and service via APIs has allowed teams to build far more complex applications than if they were to take on the risk and burden of such capabilities themselves. Now we can outsource things like authentication and identity, payments, content management, data services, search, and much more.
Jamstack sites might utilise such services at build time, and also at run time directly from the browser via JavaScript. And the clean decoupling of these services allows for greater portability and flexibility, as well as significantly reduced risk.
{{% /note %}}

# Jamstack

**J**avaScript, **A**PIs and **M**arkup

![Screenshot of the Jamstack.org website - The modern way to build websites & apps that delivers better performance](images/jamstack.png "Screenshot of the Jamstack.org website - The modern way to build websites & apps that delivers better performance")

---

{{< slide class="left-align" >}}

{{% note %}}
**Entire Project on a CDN**
Because Jamstack projects don’t rely on server-side code, they can be distributed instead of living on a single server. Serving directly from a CDN unlocks speeds and performance that can’t be beat. The more of your app you can push to the edge, the better the user experience.

**Modern Build Tools**
Take advantage of the world of modern build tools. It can be a jungle to get oriented in and it’s a fast moving space, but you’ll want to be able to use tomorrow’s web standards today without waiting for tomorrow’s browsers. And that currently means Babel, PostCSS, Webpack, and friends.

**Automated Builds**
Because Jamstack markup is prebuilt, content changes won’t go live until you run another build. Automating this process will save you lots of frustration. You can do this yourself with webhooks, or use a publishing platform that includes the service automatically.

**Atomic Deploys**
As Jamstack projects grow really large, new changes might require re-deploying hundreds of files. Uploading these one at a time can cause inconsistent state while the process completes. You can avoid this with a system that lets you do “atomic deploys,” where no changes go live until all changed files have been uploaded.

**Instant Cache Invalidation**
When the build-to-deploy cycle becomes a regular occurrence, you need to know that when a deploy goes live, it really goes live. Eliminate any doubt by making sure your CDN can handle instant cache purges.

**Everything Lives in Git**
With a Jamstack project, anyone should be able to do a git clone, install any needed dependencies with a standard procedure (like npm install), and be ready to run the full project locally. No databases to clone, no complex installs. This reduces contributor friction, and also simplifies staging and testing workflows.
{{% /note %}}

# Jamstack Recommended Practices

* Entire Project on a CDN
* Modern Build Tools
* Automated Builds
* Atomic Deploys
* Instant Cache Invalidation
* Everything Lives in Git

---

{{< slide class="left-align" >}}

{{% note %}}
## Hugo

* Uses GoLang
* Plenty of themes out there for you to get going quickly
* Great documentation
* Very fast
* Brilliant community around it
* Lots of built-in templates to get going quickly

## Jekyll

* Built using Ruby
* Has been around for some time
* Great GitHub integration - GitHub pages are powered by Jekyll!
* Great Documentation
* Can be a challenge to setup

## Gatsby

* Optimised for speed
* Uses GraphQL
* Has lots of APIs
* Documentation (?)

## Vuepress

* VueJS
* PWA Features
* Google Analytics
* Markdown to HTML

## Nuxt.JS

* VueJS framework

## Pelican

* Uses Python
* Requires Python to be installed when adding/editing content

{{% /note %}}

# Static Site Generators you may recognise…

![Screenshot showing several Static Site Generators - Hugo, Jekyll, Gatsby, Vuepress, Nuxt.JS and Pelican](images/ssgs.png "Screenshot showing several Static Site Generators - Hugo, Jekyll, Gatsby, Vuepress, Nuxt.JS and Pelican")

---

# Cloud With Chris Architecture

<img src="images/cwc-architecture.png" alt="Architecture Diagram of cloudwithchris.com. It shows that cloudwithchris.com is on Azure DNS. There is an apex domain (cloudwithchris.com) which points to Azure Front Door, and redirects to another Azure Front Door Rule (for WWW). There is a www.cloudwithchris.com subdomain which points to a WWW rule, which directs to an Azure Static Web App. There is a podcasts.cloudwithchris.com subdomain which points to a Podcast Rule, which directs to Azure Storage. There is a presentations.cloudwithchris.com subdomain which points to a Presentations Rule, which directs to an Azure Static Web App" title="Architecture Diagram of cloudwithchris.com. It shows that cloudwithchris.com is on Azure DNS. There is an apex domain (cloudwithchris.com) which points to Azure Front Door, and redirects to another Azure Front Door Rule (for WWW). There is a www.cloudwithchris.com subdomain which points to a WWW rule, which directs to an Azure Static Web App. There is a podcasts.cloudwithchris.com subdomain which points to a Podcast Rule, which directs to Azure Storage. There is a presentations.cloudwithchris.com subdomain which points to a Presentations Rule, which directs to an Azure Static Web App" width="600">

---

# Stop! Demo time.

---

{{< slide class="left-align" >}}

# How to learn more...

<div class="container">
  <div class="col">
    <p>
    <ul>
      <li><a href="https://www.cloudwithchris.com">Cloud With Chris</a></li>
      <li><a href="https://lab.github.com">GitHub Learning Labs</a></li>
      <li><a href="https://docs.microsoft.com/en-us/learn/github">Microsoft Learn</a></li>
    </ul>    
    <img src="images/cwc-site.png" alt="A screenshot of cloudwithchris.com, which shows several upcoming pieces of content" title="A screenshot of cloudwithchris.com, which shows several upcoming pieces of content" />
  </div>
  <div class="col">
    <img src="images/github-resources-follow-up.png" alt="A screenshot of GitHub Learning Lab, with a few example courses. A screenshot of Microsoft Learn, showing several example learning paths and courses" title="A screenshot of GitHub Learning Lab, with a few example courses. A screenshot of Microsoft Learn, showing several example learning paths and courses" />
  </div>
</div> 

---

# Questions?

[![Cloud With Chris logo, with a link to the website - www.cloudwithchris.com](images/cwc-banner.png "Cloud With Chris logo, with a link to the website - www.cloudwithchris.com")](https://www.cloudwithchris.com)
