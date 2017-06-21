# Instrumenting your code

## locizify

Using our locizify script is the simplest way to get your website or webapplication translated. We highly recommend using it on your static site generators like wordpress, shopify, ...

Drop one line of code:

```js
<script id="locizify" projectid="[PROJECT_ID]"
    apikey="[API_KEY]" referencelng="[LNG]"
    fallbacklng="[LNG]" saveMissing="true"
    src="https://unpkg.com/locizify@^2.0.0" />
```

*You can find your projectId and API Key in your projects settings.*

Reload your page and see the phrases ready to translate in your locize project.

Find more details and configuration options on the [github page](https://github.com/locize/locizify).