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
#   "en": {
#     "name": "English",
#     "nativeName": "English",
#     "isReferenceLanguage": true,
#     "translated": {
#       "latest": 1,
#       "production": 1
#     }
#   },
#   "de-CH": {
#     "name": "German",
#     "nativeName": "Deutsch",
#     "region": "CH",
#     "isReferenceLanguage": false,
#     "translated": {
#       "latest": 1,
#       "production": 0.521
#     }
#   },
#   "it": {
#     "name": "Italian",
#     "nativeName": "Italiano",
#     "isReferenceLanguage": false,
#     "translated": {
#       "latest": 1,
#       "production": 1
#     }
#   },
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

##### optional context:
In case you want to also save a context information for a specific translation, you can define a nested object like this:

```bash
$ body=$(cat << EOF
{
  "new.key": {
    "value: "default value",
    "context": {
      "text: "description for this key"
    }
  },
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



## Used translations

You can say to locize which translations are used. Locize will then remember at which time the translations have been last used.
For example this is very useful in development.
For example during an e2e test you can spot which translations are probably not used anymore.

This is also a HTTP POST request, with this url pattern:

`https://api.locize.io/used/{projectId}/{version}/{language}/{namespace}`

##### example:

```bash
$ body=$(cat << EOF
[
  "new.key",
  "another.new.key"
]
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/used/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
```

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

##### optional context:
In case you want to also save a context information for a specific translation, you can define a nested object like this:

```bash
$ body=$(cat << EOF
{
  "new.key": {
    "value": "default value",
    "context": {
      "text": "description for this key"
    }
  },
  "another.existing.key": "another changed value",
  "a.key.to.delete": null
}
EOF
)

$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" -d $body https://api.locize.io/missing/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
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
# "key": "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/common",
# "size": 42,
# "lastModified": "2017-11-23T19:39:16.000Z"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/landingpage",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/de/landingpage",
# "size": 21,
# "lastModified": "2017-11-23T18:39:16.000Z"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
# "size": 103,
# "lastModified": "2017-11-23T19:37:16.000Z"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/common",
# "size": 12,
# "lastModified": "2017-11-23T19:29:16.000Z"
# },
# ...
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
# "size": 236,
# "lastModified": "2017-11-24T19:39:16.000Z"
# },
# {
# url: "https://api.locize.io/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
# key: "3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production/en/common",
# "size": 417,
# "lastModified": "2017-11-23T13:39:16.000Z"
# }
# ]
```

*(You can find your projectId in your project settings under the API Tab.)*




## Fetch/filter the (unpublished) namespace resources

Sometimes in your localization process you want to know which are the translations that are approved by your reviewer.
Assuming you have defined some tags to mark translations as approved, with this api you're able to filter by these tags.

This is pretty easy. It's a simple HTTP GET request with this url pattern:

`https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}`

with positive tags filter: `https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}?tags=[0,2]` (you need to pass the tag index)

in combination with a negative tags filter: `https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}?tags=[0,2]&!tags=[1]`


Another use case could be to track the amount of words changed during a time period.
To do this, you can pull the translations at period 1, save this state and the current timestamp and later at period 2 you can pull again with an additional filter.

i.e. get all translations updated after 2017-12-06T19:42:18.139Z (UTC): `https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}?updatedAt=>1512589338139` (number of milliseconds since 1970/01/01)

i.e. get all translations updated before 2017-12-06T19:42:18.139Z (UTC): `https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}?updatedAt=<1512589338139`


Additionally another use case could be to remove unused translations. (This is only possible if you make use of the [Used translations](/api.html#used-translations) endpoint)
To do this, you can pull the translations with an additional filter.

i.e. get all translations used after 2017-12-06T19:42:18.139Z (UTC): `https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}?lastUsed=>1512589338139` (number of milliseconds since 1970/01/01)

i.e. get all translations used before 2017-12-06T19:42:18.139Z (UTC): `https://api.locize.io/pull/{projectId}/{version}/{language}/{namespace}?lastUsed=<1512589338139`




##### example:

```bash
$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/pull/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/latest/en/landingpage
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*






## Fetch configured project tags 

You may have defined some tags to mark translations as approved, etc. With this api you're able to fetch these tags.

A very simple HTTP GET request with this url pattern:

`https://api.locize.io/tags/{projectId}`

##### example:

```bash
$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/tags/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# [
# "translated",
# "reviewed",
# "approved"
# ]
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*




## Copy version

If you are using multiple versions of your translations you can ask locize to copy (replace) all translations from one version to the other.
For example this is very useful when you release your translation files from one version to the other via your custom tooling.

This is easy. It's a HTTP POST request without body with this url pattern:

`https://api.locize.io/copy/{projectId}/version/{fromVersion}/{toVersion}`

##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/copy/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/version/latest/production
$ # {"jobId":"0bb35e4a-8f16-4997-866a-1332a59825e0
"}

```

*(You can find your projectId and API Key in your project settings under the API Tab. Keep in mind to use the API Key for `{toVersion}`)*



## Publish version

If you want to fully automate your CI/CD pipeline by publishing a version exactly at the same time when you deploy a new version of your product this api call is exactly what you are looking for.

This is very easy. It's a HTTP POST request without body with this url pattern:

`https://api.locize.io/publish/{projectId}/{version}`

##### example:

```bash
$ curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/publish/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/production
$ # {"jobId":"0bb35e4a-8f16-4997-866a-1332a59825e0
"}
```

*(You can find your projectId and API Key in your project settings under the API Tab. Keep in mind to use the API Key for the correct `{version}`)*



## Get async job

To wait for an async action (i.e. [copy](https://docs.locize.com/api.html#copy-version)) to be completed, you can make use this endpoint.

It's a simple HTTP GET request without body with this url pattern:

`https://api.locize.io/jobs/{projectId}/{jobId}`

##### example:

```bash
$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/jobs/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/0bb35e4a-8f16-4997-866a-1332a59825e0
$ # {"projectId":"3d0aa5aa-4660-4154-b6d9-907dbef10bb2","jobId":"0bb35e4a-8f16-4997-866a-1332a59825e0
","event":"saveVersionRequested","startedAt":1525094049152}


```

*(You can find your projectId and API Key in your project settings under the API Tab. The jobId is returned by the async action)*





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
# "scope": {
#  "languages":["en","de"],
#  "versions":["latest","preprod"]
# },
# "link": "https://www.locize.io/register?invitation=LL4mHDzyxKn4cKYP"
# }
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*





## Fetch users

For example when you want to build your own translation management ui, this endpoint will be very useful if you want to display the project's users.

Just a HTTP GET request with this url pattern:

`https://api.locize.io/users/{projectId}`

##### example:

```bash
$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/users/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# [
#  {
#   "id":"ba175147-c7a3-45d2-9b24-739ae2ed948c",
#   "firstname": "George",
#   "lastname": "Winston",
#   "username": "gg.win",
#   "email": "george.user@somewhere-in-the-universe.com",
#   "role": "user",
#   "scope": {
#    "languages": ["en","de"],
#    "versions": ["latest","preprod"]
#   }
#  }
#  ...
# ]
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*





## Statistics: project

Do you want to show some cool overview images like this:
![](/assets/img/project_stats.png)


You can access the same data we use on the locize-client also for your own ui.

Simply make a HTTP GET request with this url pattern:

`https://api.locize.io/stats/project/{projectId}`

##### example:

```bash
$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/stats/project/3d0aa5aa-4660-4154-b6d9-907dbef10bb2
# will return something like:
# {
#    "latest":{
#       "en":{
#          "ns1":{
#             "translated":1,
#             "untranslated":0,
#             "ordered":0,
#             "segmentsTranslated":10,
#             "segmentsTotal":10
#          },
#          "anotherNamespace":{
#             "translated":1,
#             "untranslated":0,
#             "ordered":0,
#             "segmentsTranslated":1,
#             "segmentsTotal":1
#          }
#       },
#       "de":{
#          "ns1":{
#             "translated":0.7,
#             "untranslated":0.3,
#             "ordered":0,
#             "segmentsTranslated":7,
#             "segmentsTotal":10
#          },
#          "anotherNamespace":{
#             "translated":1,
#             "untranslated":0,
#             "ordered":0,
#             "segmentsTranslated":1,
#             "segmentsTotal":1
#          }
#       }
#    },
#    "prod":{
#       "en":{
#          "ns1":{
#             "translated":1,
#             "untranslated":0,
#             "ordered":0,
#             "segmentsTranslated":5,
#             "segmentsTotal":5
#          },
#          "anotherNamespace":{
#             "translated":1,
#             "untranslated":0,
#             "ordered":0,
#             "segmentsTranslated":1,
#             "segmentsTotal":1
#          }
#       },
#       "de":{
#          "ns1":{
#             "translated":1,
#             "untranslated":0,
#             "ordered":0,
#             "segmentsTranslated":5,
#             "segmentsTotal":5
#          },
#          "anotherNamespace":{
#            "translated":0.7142857142857143,
#            "untranslated":0.2857142857142857,
#            "ordered":0,
#            "segmentsTranslated":5,
#            "segmentsTotal":7
#          }
#       }
#    }
# }
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*




## Statistics: user

There are some nice statistics for users too:


Another HTTP GET request with this url pattern:

for a specific user:
`https://api.locize.io/stats/user/{projectId}/{userId}`
`https://api.locize.io/stats/user/{projectId}/{userId}?year=2018`

or for all users:
`https://api.locize.io/stats/users/{projectId}`
`https://api.locize.io/stats/users/{projectId}?year=2018`


To retrieve an other year than the current one set the query parameter `year` with the appropriate value.


##### example:

```bash
$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/stats/user/3d0aa5aa-4660-4154-b6d9-907dbef10bb2/ba175147-c7a3-45d2-9b24-739ae2ed948c
# will return something like:
# {
#    "userId":"ba175147-c7a3-45d2-9b24-739ae2ed948c",
#    "year":2018,
#    "words":{ // amount of words saved per month
#       "0":23,
#       "1":54,
#       "2":16,
#       ...
#    },
#    "tagsSet":{ // amount of tags set per month by tag index
#       "0":{
#          "2":12,
#          "4":7
#       },
#       "1":{
#          "2":5,
#          "4":18,
#          "5":21
#       },
#       "2":{
#          "4":1,
#          "5":24
#       }
#       ...
#    },
#    "tagsUnset":{ // amount of tags unset per month by tag index
#       "0":{
#          "0":2,
#          "1":7
#       },
#       "1":{
#          "0":5,
#          "1":18,
#          "2":49
#       },
#       "2":{
#          "1":10,
#          "2":34
#       }
#       ...
#    }
#    "updatedAt":1514926256221,
# }



$ curl -X GET -H "Content-Type: application/json" -H "Authorization: Bearer <API_KEY>" https://api.locize.io/stats/users/3d0aa5aa-4660-4154-b6d9-907dbef10bb2

# [
#    {
#       "userId":"ba175147-c7a3-45d2-9b24-739ae2ed948c",
#       "year":2018,
#       "words":{ // amount of words saved per month
#          "0":23,
#          "1":54,
#          "2":16,
#          ...
#       },
#       "tagsSet":{ // amount of tags set per month by tag index
#          "0":{
#             "2":12,
#             "4":7
#          },
#          "1":{
#             "2":5,
#             "4":18,
#             "5":21
#          },
#          "2":{
#             "4":1,
#             "5":24
#          }
#          ...
#       },
#       "tagsUnset":{ // amount of tags unset per month by tag index
#          "0":{
#             "0":2,
#             "1":7
#          },
#          "1":{
#             "0":5,
#             "1":18,
#             "2":49
#          },
#          "2":{
#             "1":10,
#             "2":34
#          }
#          ...
#       }
#       "updatedAt":1514926256221,
#    },
#    ...
# ]
```

*(You can find your projectId and API Key in your project settings under the API Tab.)*


