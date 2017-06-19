Migrating an existing backend from i18next is just changing a few lines of code.

# Browser

Just use the `i18next-locize-backend`

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

(You can find your projectId and API Key in your projects settings under the API Tab.)

Find more details and configuration options on the [github page](https://github.com/locize/i18next-locize-backend).

# node.js

Just use the `i18next-node-locize-backend`

```js
import i18next from 'i18next';
import Backend from 'i18next-node-locize-backend';

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

(You can find your projectId and API Key in your projects settings under the API Tab.)

Find more details and configuration options on the [github page](https://github.com/locize/i18next-node-locize-backend).

# Migrating your data

You can use our [commandline tool](https://github.com/locize/locizify-cli) to copy your existing translations over to your locize project.


