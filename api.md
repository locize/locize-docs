<!-- toc -->

# API

Do you prefer to integrate the locize api on your own?

No problem! If you want to make a low level integration or just did not found an appropriate client library here you find our simple api description or you can access API via:

- [Command Line](https://github.com/locize/locize-cli)
- [Locizer (Browser)](https://github.com/locize/locizer)

## Fetch the namespace resources

The most important feature first!

It's a simple HTTP GET request with this url pattern:

`https://api.locize.io/{projectId}/{version}/{language}/{namespace}`

##### example:

```bash
$ curl -X GET https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/landingpage
# will return something like:
# {
# "Average App": "Average App",
# "Benefits": "Benefits",
# "Blog": "Blog",
# ...
# "privacy policy": "privacy policy",
# "terms of service": "terms of service"
# }
```

*(You can find your projectId in your project settings under the API Tab.)*


## Fetch the available languages

You have the possibility to ask locize which languages are available for a particular project.
That way you can have a dynamic language selector.

It's an even simpler HTTP GET request with this url pattern:

`https://api.locize.io/languages/{projectId}`

##### example:

```bash
$ curl -X GET https://api.locize.io/languages/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# {
# "en": {
# "name": "English",
# "nativeName": "English",
# "translated": {
# "latest": 1,
# "production": 1
# }
# },
# "de-CH": {
# "name": "German",
# "nativeName": "Deutsch",
# "region": "CH",
# "translated": {
# "latest": 1,
# "production": 0.521
# }
# },
# "it": {
# "name": "Italian",
# "nativeName": "Italiano",
# "translated": {
# "latest": 1,
# "production": 1
# }
# },
# ...
# }
```

*(You can find your projectId in your project settings under the API Tab.)*


## Missing translations

You can say to locize that some translations are missing.
For example this is very useful in development.
This will not replace an existing translation.

This is a little bit more advanced. It's a HTTP POST request with this url pattern:

`https://api.locize.io/missing/{projectId}/{version}/{language}/{namespace}`

##### example:

```bash
$ body=$(cat << EOF
{
"new.key": "default value",
"another.new.key": "another default value"
}
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/missing/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
```

***Advice:***
- *Translations not defined in your reference language will not be shown in the locize app.*
- *You should post missing translation to the reference language first!*

*(You can find your projectId and API Key in your project settings under the API Tab.)*


## Update/Remove translations

You can say to locize that some translations should be updated or deleted.
For example this is very useful for an integration from an other already existing system to slowly transition the translations to locize.

This is also a little bit more advanced. It's a HTTP POST request with this url pattern:

`https://api.locize.io/update/{projectId}/{version}/{language}/{namespace}`

To completely replace a namespace set the query parameter `replace` to true. This will empty the namespace before saving the new translations.

##### example:

```bash
$ body=$(cat << EOF
{
"new.key": "default value",
"another.existing.key": "another changed value",
"a.key.to.delete": null
}
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/update/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage

$ # or:
$ # curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/update/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage?replace=true

```

*(You can find your projectId and API Key in your project settings under the API Tab.)*


## List all namespace resources

If you need an overview of all published translation files of your project, you can do this with a simple HTTP GET request with this url pattern:

`https://api.locize.io/download/{projectId}/{version}/{language}/{namespace}`

{namespace}, {language} and {version} are optional and are used as filter.

##### example:

```bash
$ curl -X GET https://api.locize.io/download/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# [
# {
# "url": "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/common",
# "key": "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/common"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/landingpage",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/landingpage"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common"
# },
# ...
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common"
# }
# ]
```

*(You can find your projectId in your project settings under the API Tab.)*



## Copy version

If you are using multiple versions of your translations you can ask locize to copy (replace) all translations from one version to the other.
For example this is very useful when you release your translation files from one version to the other via your custom tooling.

This is easy. It's a HTTP POST request without body with this url pattern:

`https://api.locize.io/copy/{projectId}/version/{fromVersion}/{toVersion}`

##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/copy/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/version/latest/production
```

*(You can find your projectId and API Key in your project settings under the API Tab. Keep in mind to use the API Key for `{toVersion}`)*



## Publish version

If you want to fully automate your CI/CD pipeline by publishing a version exactly at the same time when you deploy a new version of your product this api call is exactly what you are looking for.

This is very easy. It's a HTTP POST request without body with this url pattern:

`https://api.locize.io/publish/{projectId}/{version}`

##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/publish/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production
```

*(You can find your projectId and API Key in your project settings under the API Tab. Keep in mind to use the API Key for the correct `{version}`)*



---


>Sometimes you want to automate even more. I.e if you want to create your own translation management ui.
> The following endpoints are probably what you are looking for.


## Create a new namespace

`https://api.locize.io/create/{projectId}/{version}/{language}/{namespace}`

A body containing initial values is optional.

##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/create/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*



## Rename a namespace in all languages

`https://api.locize.io/rename/{projectId}/{version}/{fromNamespace}/{toNamespace}`


##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/rename/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/landingpage/landingpagenew
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*





## Delete a namespace from all languages

`https://api.locize.io/delete/{projectId}/{version}/{namespace}`


##### example:

```bash
$ curl -X DELETE -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/delete/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/landingpage
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*




## Add new language

`https://api.locize.io/language/{projectId}/{language}`


##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/language/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/en
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*



## Remove language

`https://api.locize.io/language/{projectId}/{language}`


##### example:

```bash
$ curl -X DELETE -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/language/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/en
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*



## Invite new users

`https://api.locize.io/invite/{projectId}`

The body contains
- **email** the user's email address
- **role** can be `"user"` or `"admin"` (default: `"user"`)
- **scope** is an object describing a scope restriction (default: empty arrays for languages and versions)

To skip sending the email automatically set the query parameter `send` to false. This will not send any email. This way you can send the invitation mail by your own, if you want to.





##### example:

```bash
$ body=$(cat << EOF
{
"email": "new.user@somewhere-in-the-universe.com",
"role": "user",
"scope": {
"languages": ["en","de"],
"versions": ["latest","preprod"]
}
}
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/invite/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
$ # or:
$ # curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/invite/3d0aa5aa-4660-4154-b6d9-907dbef10bb2?send=false
# will return something like:
# {
# "code": "LL4mHDzyxKn4cKYP",
# "role": "user",
# "email": "new.user@somewhere-in-the-universe.com",
# "scope": {"languages":["en","de"],"versions":["latest","preprod"]},
# "link": "https://www.locize.io/register?invitation=LL4mHDzyxKn4cKYP"
# }
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*