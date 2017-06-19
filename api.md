<!-- toc -->
# API

Do you prefer to integrate the locize api on your own?

No problem! If you want to make a low level integration or just did not found an appropriate client library here you find our simple api description or you can access API via:

- [Command Line](https://github.com/locize/locize-cli)
- [Locizer (Browser)](https://github.com/locize/locizer)

## Fetch the namespace resources
{% method %}

The most important feature first!

It's a simple HTTP GET request with this url pattern:

`https://api.locize.io/{projectId}/{version}/{language}/{namespace}`

##### example:

{% sample lang="bash" %}

```bash
$ curl -X GET https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/landingpage
# will return something like:
# {
#   "Average App": "Average App",
#   "Benefits": "Benefits",
#   "Blog": "Blog",
#   ...
#   "privacy policy": "privacy policy",
#   "terms of service": "terms of service"
# }
```

*(You can find your projectId in your project settings under the API Tab.)*

{% endmethod %}


## Fetch the available languages
{% method %}

You have the possibility to ask locize which languages are available for a particular project.
That way you can have a dynamic language selector.

It's an even simpler HTTP GET request with this url pattern:

`https://api.locize.io/languages/{projectId}`

##### example:

{% sample lang="bash" %}

```bash
$ curl -X GET https://api.locize.io/languages/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# {
#   "en": {
#     "name": "English",
#     "nativeName": "English",
#     "translated": {
#       "latest": 1,
#       "production": 1
#     }
#   },
#   "de-CH": {
#     "name": "German",
#     "nativeName": "Deutsch",
#     "region": "CH",
#     "translated": {
#       "latest": 1,
#       "production": 0.521
#     }
#   },
#   "it": {
#     "name": "Italian",
#     "nativeName": "Italiano",
#     "translated": {
#       "latest": 1,
#       "production": 1
#     }
#   },
#   ...
# }
```

*(You can find your projectId in your project settings under the API Tab.)*

{% endmethod %}


## Missing translations
{% method %}

You can say to locize that some translations are missing.
For example this is very useful in development.
This will not replace an existing translation.

This is a little bit more advanced. It's a HTTP POST request with this url pattern:

`https://api.locize.io/missing/{projectId}/{version}/{language}/{namespace}`

##### example:

{% sample lang="bash" %}

```bash
$ body=$(cat  << EOF
{
    "new.key": "default value",
    "another.new.key": "another default value"
}
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer mysecret-very-4f2e-b123-d432d86430c6" -d $body https://api.locize.io/missing/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*

{% endmethod %}


## Update/Remove translations
{% method %}

You can say to locize that some translations should be updated or deleted.
For example this is very useful for an integration from an other already existing system to slowly transition the translations to locize.

This is also a little bit more advanced. It's a HTTP POST request with this url pattern:

`https://api.locize.io/update/{projectId}/{version}/{language}/{namespace}`

##### example:

{% sample lang="bash" %}

```bash
$ body=$(cat  << EOF
{
    "new.key": "default value",
    "another.existing.key": "another changed value",
    "a.key.to.delete": null
}
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer mysecret-very-4f2e-b123-d432d86430c6" -d $body https://api.locize.io/update/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*

{% endmethod %}


## List all namespace resources
{% method %}

If you need an overview of all published translation files of your project, you can do this with a simple HTTP GET request with this url pattern:

`https://api.locize.io/download/{projectId}/{version}/{language}/{namespace}`

{namespace}, {language} and {version} are optional and are used as filter.

##### example:

{% sample lang="bash" %}

```bash
$ curl -X GET https://api.locize.io/download/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# [
#   {
#     "url": "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/common",
#     "key": "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/common"
#   },
#   {
#     url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/landingpage",
#     key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/landingpage"
#   },
#   {
#     url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
#     key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common"
#   },
#   {
#     url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
#     key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common"
#   },
#   ...
#   {
#     url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
#     key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common"
#   },
#   {
#     url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
#     key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common"
#   }
# ]
```

*(You can find your projectId in your project settings under the API Tab.)*

{% endmethod %}



## Copy version
{% method %}

If you are using multiple versions of your translations you can ask locize to copy (replace) all translations from one version to the other.
For example this is very useful when you release your translation files from one version to the other via your custom tooling.

This is easy. It's a HTTP POST request without body with this url pattern:

`https://api.locize.io/copy/{projectId}/version/{fromVersion}/{toVersion}`

##### example:

{% sample lang="bash" %}

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer mysecret-very-4f2e-b123-d432d86430c6" https://api.locize.io/copy/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/version/latest/production
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*

{% endmethod %}