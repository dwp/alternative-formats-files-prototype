# Alternative contact formats plugin for the GOV.UK prototype kit

A plugin user flow for alternative contact formats, for use with the [GOV.UK Prototype Kit](https://prototype-kit.service.gov.uk/docs/).

This plugin allows you to insert the full [DWP Choose alternative contact formats pattern](https://design-system.dwp.gov.uk/patterns/alternative-formats) into a prototype with minimal coding. It includes pages, routes and logic for collecting information about users' written and spoken contact needs.

## Requirements

To use this plugin, first start a prototype by installing the GOV.UK Prototype Kit (version 13 or later).

### 1. Install the plugin

In the folder that contains your prototype, install the plugin by running the following terminal command:

```bash
npm install https://github.com/dwp/alternative-formats-plugin
```

### 2. Add the following code to your prototype's app/routes.js file

```js
const alternativeFormatsPlugin = require("alternative-formats-plugin");

alternativeFormatsPlugin(router);
```

### 3. Add the pattern to your prototype

Link or redirect from any page in your prototype as shown below. In this example the link is a "Continue" button.

```jinja

{# Example of a Continue button #}
{{ 
    govukButton({
        text: "Continue",
        href: "/dwp-alternative-formats-plugin/start?alternative_formats_exit_url=/your-exit-url",
        isStartButton: false
    })
}}
```

This link also controls what happens next when the user finishes choosing contact formats. In the link, replace `/your-exit-url` with the URL that should load when the user selects "Continue" on the last page of the pattern (the Check answers page).

(See [Use links to set data](https://prototype-kit.service.gov.uk/docs/pass-data#use-links-to-set-data) for more about how this works.)

The user's answers are stored in the browser session and will be cleared (along with any other stored session data) by the "Clear data" link in the prototype footer.

### 4. Override the plugin views' content, style or redirect to a different page.

1. Go to the page of the plugin you want to override and make a note of its url. For instance, if you want to change we want to change the phone call options page, the url is `/dwp-alternative-formats-plugin/v2/journey-1/phone-call-options`.

2. Create a new version of the phone call options page that contains your changes. Then go to the `app/routes.js` of your prototype and write a new route for your new phone call options page. Make sure you place the new route _before_ the code you copied in step 2. It could be something like this:

```
router.get("/dwp-alternative-formats-plugin/v2/journey-1/phone-call-options", (req, res) => {
  res.render("my-new-phone-call-options.njk");
});
```

3. The plugin will work in the same way as before, but now it will show your new phone call options page when that url is visited.
