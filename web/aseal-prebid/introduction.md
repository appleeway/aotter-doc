# Introduction

Welcome👋🏼

In this section, we will introduce some basic knowledge about Prebid. Also, it explains how to integrate with **Aseal**’s Direct Bidder solution in your **existing Prebid** campaign.&#x20;

If you are starting a Prebid implementation from scratch, please refer to Prebid's _How-to_ documentation [here](http://prebid.org/overview/intro.html).&#x20;

### What is Prebid?

Prebid provides an open-source **header bidding solution** that is scalable and allows digital publishers to use real-time auctions mechanisms to maximize yield from their web and mobile app inventories. It is a whole ecosystem for standardizing header bidding and includes a product suite, a community, and an organization.

Prebid product suite consists of three important components:

* **Prebid.js(wrapper)**
* Prebid Server
* Prebid Mobile

Prebid Server / Prebid Mobile won’t be covered in this document, if you are interested in these two topics please refer to the link below.

> * [https://docs.prebid.org/prebid-server/overview/prebid-server-overview.html](https://docs.prebid.org/prebid-server/overview/prebid-server-overview.html)
> * [https://docs.prebid.org/prebid-mobile/prebid-mobile.html](https://docs.prebid.org/prebid-mobile/prebid-mobile.html)

### What is **Prebid.js?**

**Prebid.js is an open-source header bidding wrapper that helps you connect with multiple demand partners at once**, run header auctions, and serve ads from the highest bidder in real-time. \
With Prebid.js, you can easily set up line items in **Google Ad Manager**, send asynchronous ad requests to bidding partners, and manage them effectively.

### How does Prebid.js differ from **Prebid Adapter**?

As we explained above, Prebid.js is a header bidding wrapper that connects you to multiple demand partners. On the other hand, **Prebid Adapter is a specific code provided by the demand partner** (SSP or Ad Exchange) **that enables you to integrate it with your wrapper.**&#x20;
