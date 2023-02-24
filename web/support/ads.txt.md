# ads.txt

### Implementing ads.txt in your website following steps:

#### **Step 1.**[**Overview**](ads.txt.md#overview)****

#### **Step 2.**[**Set up an ads.txt file**](ads.txt.md#set-up-an-app.txt-file)****

#### **Step 3.**[**Publish your ads.txt file on your website**](ads.txt.md#publish-your-ads.txt-file-on-your-website)****

## [Overview](ads.txt.md#step-1.overview)

[Authorized Digital Sellers, or ads.txt](https://iabtechlab.com/ads-txt/) is an IAB Tech Lab initiative that helps ensure that your digital ad inventory is only sold through sellers (such as AdSense) who you've identified as authorized. Creating your own ads.txt file gives you more control over who's allowed to sell ads on your site and helps prevent counterfeit inventory from being presented to advertisers.

The ads.txt files are publicly available and crawlable by exchanges, supply-side platforms (SSP), and other buyers and third-party vendors.

The mission of the ads.txt is simple: Increase transparency in the programmatic advertising ecosystem. ads.txt stands for Authorized Digital Sellers and is a simple, flexible and secure method that publishers and distributors can use to publicly declare the companies they authorize to sell their digital inventory.

This is a ads.txt file example:

{% hint style="warning" %}
**Note**: Your ads.txt file must be formatted as specified by the IAB Tech Lab in order to be verified. If you need additional help, review the [ads.txt Specification](https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1.pdf) provided by the IAB Tech Lab.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/app-ads.png" alt=""><figcaption></figcaption></figure>

## [Set up an ads.txt file](ads.txt.md#step-2.set-up-an-ads.txt-file)

* If you haven't already ,we provide ads.txt file for publisher download.

{% file src="../../.gitbook/assets/ads.txt" %}

## [Publish your ads.txt file on your website](ads.txt.md#step-3.publish-your-ads.txt-file-on-your-website)

The hostname is determined from your website.Here is a example.

| Format                                                                                                  | Example                         |
| ------------------------------------------------------------------------------------------------------- | ------------------------------- |
| **https://<\<hostname>>/ads.txt**[&#xD;](https://example.com/app-ads.txthttp://example.com/app-ads.txt) | **https://example.com/ads.txt** |
| **http://<\<hostname>>/ads.txt**                                                                        | **http://example.com/ads.txt**  |
