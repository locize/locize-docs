<!-- toc -->

# Webhook

Get directly notified on a webhook url if something noticeable happens.

To enable this service go to settings, select the services tab and configure your endpoint.
Make sure you have a secure https endpoint. 

The following messages will be sent as json payload with a POST request.

*You should respond with a successful http status code 200 within 10 seconds.*

All messages will have the following structure:
```json
{
   "id":"830fbcbb-90b7-4f0f-86bb-c82b55aab385", // the message id
   "name":"dummyTestEvent", // the message name
   "occurredAt":"2018-01-02T20:05:59.008Z", // the moment when this message occurred in ISO 8601 format
   "message":"William Timberland just added a webhook to THIS PROJECT!", // a descriptive text of this message
   "payload":{ // a variable payload
      "messageTypes":[
         "languageAdded",
         "languageDeleted",
         "versionAdded",
         "versionDeleted",
         "referenceLanguageChanged",
         "orderCreated",
         "orderCompleted",
         "invitationAccepted",
         "versionPublished",
         "versionOverwrote",
         "namespaceAdded",
         "namespaceDeleted",
         "namespaceCompleted",
         "namespaceNotCompletedAnymore"
      ]
   },
   "meta":{ // a meta object containing...
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6", // the project id
         "name":"THIS PROJECT", // the project name
         "slug":"albo6dxk" // the project slug
      },
      "user":{ // if message issued by a user
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a", // the user id
         "firstname":"William", // the user firstname
         "lastname":"Timberland" // the user lastname
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest" // a link pointing to the locize client
   }
}
```



## languageAdded

```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"languageAdded",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland added language de!",
   "payload":{
      "language":"de"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## languageDeleted
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"languageDeleted",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland removed language de!",
   "payload":{
      "language":"de"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## versionAdded
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"versionAdded",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland added version prod!",
   "payload":{
      "version":"prod"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## versionDeleted
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"versionDeleted",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland removed version prod!",
   "payload":{
      "version":"prod"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## referenceLanguageChanged
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"referenceLanguageChanged",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland changed reference language from en to de!",
   "payload":{
      "from":"en",
      "to":"de"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## orderCreated
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"orderCreated",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland created a translation order with gengo!",
   "payload":{
      "service":"gengo",
      "version":"latest"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## orderCompleted
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"orderCompleted",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"gengo order completed!",
   "payload":{
      "service":"gengo",
      "version":"latest"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "link":"https://www.locize.io/p/albo6dxk/orders"
   }
}
```

## invitationAccepted
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"invitationAccepted",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland accepted the invitation and is now part of your project!",
   "payload":{},
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## versionPublished
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"versionPublished",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland published version prod!",
   "payload":{
      "version":"prod"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/prod"
   }
}
```

## versionOverwrote
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"versionOverwrote",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland overwrote version prod with test!",
   "payload":{
      "from":"test",
      "to":"prod"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/prod"
   }
}
```

## namespaceAdded
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"namespaceAdded",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland added namespace landingpage in version latest!",
   "payload":{
      "namespace":"landingpage",
      "version":"latest"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## namespaceDeleted
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"namespaceDeleted",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"William Timberland removed namespace landingpage in version latest!",
   "payload":{
      "namespace":"landingpage",
      "version":"latest"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "user":{
         "id":"ab075147-c7a3-45d2-9b24-739ae2ed948a",
         "firstname":"William",
         "lastname":"Timberland"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest"
   }
}
```

## namespaceCompleted
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"namespaceCompleted",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"Translation of namespace landingpage in language en for version latest completed!",
   "payload":{
      "namespace":"landingpage",
      "language":"en",
      "version":"latest"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest/en/landingpage"
   }
}
```

## namespaceNotCompletedAnymore
```json
{
   "id":"427cc4dd-adf5-4fb8-ad8d-8508f2788fe3",
   "name":"namespaceNotCompletedAnymore",
   "occurredAt":"2018-01-02T21:27:11.326Z",
   "message":"New segments of namespace landingpage ready to be translated in language en for version latest!",
   "payload":{
      "namespace":"landingpage",
      "language":"en",
      "version":"latest"
   },
   "meta":{
      "project":{
         "id":"23dad587-b3bf-4663-b15c-ad8d66213ac6",
         "name":"THIS PROJECT",
         "slug":"albo6dxk"
      },
      "link":"https://www.locize.io/p/albo6dxk/v/latest/en/landingpage"
   }
}
```







