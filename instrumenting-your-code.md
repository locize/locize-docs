<!-- toc -->

# Instrumenting your code

## locizify

Using our locizify script is the simplest way to get your website or webapplication translated. We highly recommend using it on your static site generators like wordpress, shopify, ...

<img src="/assets/img/locizify-frameworks.png" width="80%" />


Drop one line of code:

```js
<script
    id="locizify" projectid="[PROJECT_ID]"
    apikey="[API_KEY]" referencelng="[LNG]"
    fallbacklng="[LNG]" saveMissing="true"
    src="https://unpkg.com/locizify@^2.0.0"
></script>
```

*You can find your projectId and API Key in your projects settings.*

Reload your page and see the phrases ready to translate in your locize project.

Find more details and configuration options on the [github page](https://github.com/locize/locizify).


## i18next

You can use locize in combination with i18next. I18next is a well known internationalization framework and offers a wide range of framework integrations and plugins for almost every need.

<img src="/assets/img/i18next-frameworks.png" width="80%" />

[Learn more about i18next](http://i18next.com)

To connect i18next with the locize service integrate the xhr or node.js backend:

```js
import i18next from 'i18next';
import Backend from 'i18next-locize-backend';

i18next
  .use(Backend)
  .init({
    // ...other options
    backend: {
      projectId: '[PROJECT_ID]',
      apiKey: '[API_KEY]',
      referenceLng: '[LNG]'
    }
  });
```

browser: [Learn more about the browser backend](https://github.com/locize/i18next-locize-backend)

nodejs: [Learn more about the nodejs backend](https://github.com/locize/i18next-node-locize-backend)

Checkout our [samples](https://github.com/locize/locize-examples).

## other options

### clientside: polyglot, formatjs, react-intl, js-lingui, messageformat, ...

You can use our locizer script to load translations from locize and add them to your i18n framework in the browser:

Sample for polyglot:

```js
// <script src="https://unpkg.com/locizer/locizer.min.js"></script>
locizer
  .init({
    fallbackLng: 'en',
    referenceLng: 'en',
    projectId: '[your project id]'
  })
  .load('translation', function(err, translations, lng) {
    const polyglot = new Polyglot({ phrases: translations, locale: lng });
    console.log(polyglot.t('some key'));
  });
```

For more details checkout [locizer docs](https://github.com/locize/locizer)

Our samples:

- [formatjs](https://github.com/locize/locize-formatjs-example)
- [polyglot](https://github.com/locize/locize-polyglot-example)
- [js-lingui](https://github.com/locize/locize-js-lingui-example)

### serverside

For js environments please watch out for the i18next integration options.

On other environments you could use:

- [Our API](/api.md)
- [Our locize-cli](https://github.com/locize/locize-cli)

### other formats xliff, gettext, ...

You can use following modules to convert between formats:

- [xliff](https://github.com/locize/xliff)
- [android-string-resource](https://github.com/locize/android-string-resource)
- [gettext (.mo/.po](https://github.com/i18next/i18next-gettext-converter)

Simplest is to use those in combination with our [cli](https://github.com/locize/locize-cli) to build an automated production pipeline powered by grunt, gulp, npm script, ...
