<!--yml
category: 未分类
date: 2024-05-18 05:28:43
-->

# SAML Madness | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/11/03/saml-madness/#0001-01-01](https://mdavey.wordpress.com/2016/11/03/saml-madness/#0001-01-01)

## SAML Madness

Recently when doing some investigation into the world of [SAML](http://saml.xml.org/wiki/sp-initiated-single-sign-on-postartifact-bindings), I found the SAML Chrome [Panel](https://chrome.google.com/webstore/detail/saml-chrome-panel/paijfdbeoenhembfhkhllainmocckace) useful.  Also found “OAuth with SAML2.0 Authentication” help – I particularly like [sequence](http://blog.scottlogic.com/2015/11/19/oauth2-with-saml2.html) diagrams 🙂

Once the browser has the SAMLResponse post authentication, it will hit the original web server the User Agent was requesting via a POST – make sure you know what URL the browser is POSTing to 🙂

~ by mdavey on November 3, 2016.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [SAML](https://mdavey.wordpress.com/tag/saml/)