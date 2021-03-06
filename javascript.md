---
description: A guide for Weglot's client Javascript integration
---

# Javascript

## Getting started

Let's include Weglot's client code into your site and get started with translations.

1. Go to your Weglot dashboard \([https://dashboard.weglot.com/](https://dashboard.weglot.com/)\) and get your API key in the "Project settings" menu \(e.g. `wg_1234567897e2ea993d291b571c2ec93b0`\)
2. Edit your HTML file, and right after the`<body>`tag, append the following code:

```markup
<script type="text/javascript" src="https://cdn.weglot.com/weglot.min.js"></script>
<script>
	Weglot.setup({
	  api_key: 'YOUR_API_KEY',
	  originalLanguage: 'en',
	  destinationLanguages : 'fr,es',
	 });
</script>
```

Make sure you replace `YOUR_API_KEY`with the API key you got in the step one.

You can now refresh your page. French and Spanish are now translation options for your website in English!

{% hint style="info" %}
The full list of language codes we support is available at [https://weglot.com/documentation/available-languages](https://weglot.com/documentation/available-languages)
{% endhint %}

## Initialization code

As you've seen in the "Getting started" section, Weglot gets initialized through this code:

```javascript
Weglot.setup(options)
```

Where `options` is a Javascript object with properties defined as follows. Only **api\_key**, **originalLanguage** and **destinationLanguages** are mandatory.

* **`api_key`**: your Weglot API key
* **`originalLanguage`**: the ISO 639-1 2-letter code of the original language of your website
* **`destinationLanguages`**: a comma-separated list of 2-letter codes of languages you wish to be able to translate your website to
* `styleOpt` is a javascript object describing the default styling of the Weglot language switcher button:
  * `withname`: `1` or `true` to display a label text next to each language options. `0` or `false` otherwise
  * `fullname`: If `withname` is true, `1` or `true` to display the full name of the language. `0` or `false` to just show the 2-letter language code.
  * `is_dropdown`: `1` or `true` to display the language selector as a dropdown. `0` or `false` to show it as a list
  * `classF`: the extra CSS class to apply to the button elements. Add `wg-flags` to show flags \(by default they will be mat rectangles\).
    * Add `flag-1` for the flags to be rectangle bright
    * Add `flag-2` for the flags to be squares
    * Add `flag-3` for the flags to be circles
* `autoSwitch`: `1` or `true` to automatically switch to the user's preferred language if available. `0` or `false` otherwise. Defaults to `0`.
* `exceptions`: A comma-separated list of CSS selectors of elements to exempt from translation
* `dynamic`: A comma-separated list of CSS selectors of elements to dynamically watch for changes of for automatic translations
* `searchForms`: A comma-separated list of CSS selectors of search form elements to watch for. Useful if translateSearch is true.
* `excludePaths`: A comma-separated list of paths to exclude from translations. It's a regex string that the current path will be tested against.
* `waitTransition`: `1` or `true` to prevent content blinking when translating a new page. Defaults to `false`.
* `translateSearch`: `1` or `true` to translate search queries on the website, `O` or `false` otherwise. Defaults to `false`.
* `switchers`: A javascript Array of Objects with the following properties:
  * `styleOpt`: defined exactly as the main styleOpt
  * `target`: the CSS selector of the node that the switcher will be a child of
  * `sibling`: the CSS selector of the next sibling element of the switcher. `null` for last element inside the target

A full example could look like this:

```javascript
Weglot.setup({
  api_key: "wg_1234567897e2ea993d291b571c2ec93b0",
  originalLanguage: "en",
  destinationLanguages : "ar,fr",
  styleOpt : { fullname: true , withname: true , is_dropdown: true , classF: "wg-flags flag-3" },
  exceptions: "#not-this-element,.not-this-class.p",
  excludePaths: "",
  dynamic: ".a-container-of-dynamic-content",
  autoSwitch: true,
  translateSearch: false,
  switchers: [
    {
      styleOpt:{
        fullname: true,
        withname: true,
        is_dropdown: true,
        classF: "wg-flags flag-3"
      },
      containerCss: "",
      target: ".site-header__section--title",
      sibling: null
    }
  ]
});
```

## JS Library versions

Weglot's JS library comes in different versions. They are all stored in our CDN in a minified file.

Depending on the version you would like to use, you may want to change first line of code in the "Getting started" section. For example, to use the standard version of Weglot JS \(which is available at https://cdn.weglot.com/weglot.min.js\), the first line will be:

```markup
<script type="text/javascript" src="https://cdn.weglot.com/weglot.min.js"></script>
```

### **Standard**

Available at _https://cdn.weglot.com/weglot.min.js_

Use this version when you're not installing Weglot on one of our supported platforms \(Shopify, Wix, Bigcommerce, etc.\)

### Shopify

Available at _https://cdn.weglot.com/weglot\_shopify.min.js_ 

This is the version used by Weglot's [Shopify app](https://apps.shopify.com/weglot). It's included automatically for you, hence we advise you to use our app directly for any Shopify store as some features come only from the app \(Checkout translation, drag-and-drop placement, etc.\)

This version adds a few Shopify-specific options and features, sets the user language for each order and integrates to the right

### **Bigcommerce**

Available at _https://cdn.weglot.com/weglot\_bigcommerce.min.js_

This is the version used by the [Bigcommerce app](https://www.bigcommerce.com/apps/weglot-translate/). It adds some convenience options that help setting the right customer language along the way, as well as support for cart drawers.

### **Wix**

Available at _https://cdn.weglot.com/weglot\_wix.min.js_

This is the version any Wix user should use, as it loads the Weglot app once the Wix website has been initialised properly.

### **Jimdo**

Available at _https://cdn.weglot.com/weglot\_jimdo.min.js_

This is the version any Jimdo user should use.

