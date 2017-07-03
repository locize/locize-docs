<!-- toc -->

# Supported Formats

We work on extending the list of formats supported. If you need a format and can't find it here send us an [email](mailto:support@locize.com).

## Import

### JSON nested

JSON format nested by keys separated by `.`:

```json
{
  "appName": "locize.com - localization as a service",
  "label": {
    "cancel": "cancel",
    "save": "save"
  }
}
```

### JSON flatten

JSON format flatten - ignoring `.` separation:

```json
{
  "appName": "locize.com - localization as a service",
  "label.cancel": "cancel",
  "label.save": "save"
}
```

### CSV

Comma separated values - optimal reusing the previously exported files including added translations.

```txt
"key","de","en"
"appName","locize.com - Lokalisierung als Service","locize.com - localization as a service"
"label.cancel","abbrechen","cancel"
"label.save","speichern","save"
```



## Export

### JSON nested

Will export in JSON format nesting keys separated by `.`:

```json
{
  "appName": "locize.com - localization as a service",
  "label": {
    "cancel": "cancel",
    "save": "save"
  }
}
```

### JSON flatten

Will export in JSON format flat ignoring `.` separation:

```json
{
  "appName": "locize.com - localization as a service",
  "label.cancel": "cancel",
  "label.save": "save"
}
```

### CSV

Exports reference language and target language in one file. This format is also supported for imports and is an option to send translations to freelancers not supporting xliff or other formats.

```txt
"key","de","en"
"appName","locize.com - Lokalisierung als Service","locize.com - localization as a service"
"label.cancel","abbrechen","cancel"
"label.save","speichern","save"
```

### yaml

Yaml is a alternative format to json.

```yaml
appName: locize.com - localization as a service
label.cancel: cancel
label.save: save
```

### xliff 1.2

Well known translation exchange format.

```xml
<xliff xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="urn:oasis:names:tc:xliff:document:1.2 http://docs.oasis-open.org/xliff/v1.2/os/xliff-core-1.2-strict.xsd" xmlns="urn:oasis:names:tc:xliff:document:1.2" version="1.2">
  <file original="formats" datatype="plaintext" source-language="de" target-language="en">
    <body>
      <trans-unit id="appName">
        <source>locize.com - Lokalisierung als Service</source>
        <target>locize.com - localization as a service</target>
      </trans-unit>
      <trans-unit id="label.cancel">
        <source>abbrechen</source>
        <target>cancel</target>
      </trans-unit>
      <trans-unit id="label.save">
        <source>speichern</source>
        <target>save</target>
      </trans-unit>
    </body>
  </file>
</xliff>
```

### xliff 2.0

Well known translation exchange format. Used format on iOS.

```xml
<xliff xmlns="urn:oasis:names:tc:xliff:document:2.0" version="2.0" srcLang="de" trgLang="en">
  <file id="formats">
    <unit id="appName">
      <segment>
        <source>locize.com - Lokalisierung als Service</source>
        <target>locize.com - localization as a service</target>
      </segment>
    </unit>
    <unit id="label.cancel">
      <segment>
        <source>abbrechen</source>
        <target>cancel</target>
      </segment>
    </unit>
    <unit id="label.save">
      <segment>
        <source>speichern</source>
        <target>save</target>
      </segment>
    </unit>
  </file>
</xliff>
```

### Android resource string

Format used on Android.

```xml
<resources>
  <string name="appName">locize.com - localization as a service</string>
  <string name="label.cancel">cancel</string>
  <string name="label.save">save</string>
</resources>
``











