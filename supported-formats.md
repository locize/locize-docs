<!-- toc -->

# Supported Formats

We work on extending the list of formats supported. If you need a format and can't find it here send us an [email](mailto:support@locize.com).

## Import / Export

### JSON nested

Will import / export in JSON format nesting keys separated by `.`:

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

Will import / export in JSON format flat ignoring `.` separation:

```json
{
  "appName": "locize.com - localization as a service",
  "label.cancel": "cancel",
  "label.save": "save"
}
```

### CSV

Exports reference language and target language in one file. This format is also supported for imports and is an option to send translations to freelancers not supporting xliff or other formats.

For optimal import reuse the previously exported files including added translations.


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
```

### Gettext po files

Gettext standard format.

```po
msgid ""
msgstr ""
"Project-Id-Version: locize: My project - translations\n"
"MIME-Version: 1.0\n"
"Content-Type: text/plain; charset=utf-8\n"
"Content-Transfer-Encoding: 8bit\n"
"Plural-Forms: nplurals=2; plural=(n != 1)\n"
"POT-Creation-Date: 2017-07-14T22:26:46.631Z\n"
"PO-Revision-Date: 2017-07-14T22:26:46.631Z\n"
"Language: it\n"

msgid "title"
msgstr "La soluzione migliore per il miglior cliente!"

msgid "description"
msgstr ""
"S est Lorem ipsum dolor sit amet. Il cammino è morto, a duo dolores ed a "
"rebum. Stet clita kasd gubergren, senza mare incontro sanctus est Lorem "
"ipsum dolor sit amet."
```

### resx Files (.net)

Localizations file used in .net framework

```xml
<?xml version="1.0" encoding="utf-8"?>
<root>
  <!--
    Microsoft ResX Schema

    Version 2.0

    The primary goals of this format is to allow a simple XML format
    that is mostly human readable. The generation and parsing of the
    various data types are done through the TypeConverter classes
    associated with the data types.

    Example:

    ... ado.net/XML headers & schema ...
    <resheader name="resmimetype">text/microsoft-resx</resheader>
    <resheader name="version">2.0</resheader>
    <resheader name="reader">System.Resources.ResXResourceReader, System.Windows.Forms, ...</resheader>
    <resheader name="writer">System.Resources.ResXResourceWriter, System.Windows.Forms, ...</resheader>
    <data name="Name1"><value>this is my long string</value><comment>this is a comment</comment></data>
    <data name="Color1" type="System.Drawing.Color, System.Drawing">Blue</data>
    <data name="Bitmap1" mimetype="application/x-microsoft.net.object.binary.base64">
        <value>[base64 mime encoded serialized .NET Framework object]</value>
    </data>
    <data name="Icon1" type="System.Drawing.Icon, System.Drawing" mimetype="application/x-microsoft.net.object.bytearray.base64">
        <value>[base64 mime encoded string representing a byte array form of the .NET Framework object]</value>
        <comment>This is a comment</comment>
    </data>

    There are any number of "resheader" rows that contain simple
    name/value pairs.

    Each data row contains a name, and value. The row also contains a
    type or mimetype. Type corresponds to a .NET class that support
    text/value conversion through the TypeConverter architecture.
    Classes that don't support this are serialized and stored with the
    mimetype set.

    The mimetype is used for serialized objects, and tells the
    ResXResourceReader how to depersist the object. This is currently not
    extensible. For a given mimetype the value must be set accordingly:

    Note - application/x-microsoft.net.object.binary.base64 is the format
    that the ResXResourceWriter will generate, however the reader can
    read any of the formats listed below.

    mimetype: application/x-microsoft.net.object.binary.base64
    value   : The object must be serialized with
            : System.Runtime.Serialization.Formatters.Binary.BinaryFormatter
            : and then encoded with base64 encoding.

    mimetype: application/x-microsoft.net.object.soap.base64
    value   : The object must be serialized with
            : System.Runtime.Serialization.Formatters.Soap.SoapFormatter
            : and then encoded with base64 encoding.

    mimetype: application/x-microsoft.net.object.bytearray.base64
    value   : The object must be serialized into a byte array
            : using a System.ComponentModel.TypeConverter
            : and then encoded with base64 encoding.
    -->
  <xsd:schema id="root" xmlns="" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">
    <xsd:import namespace="http://www.w3.org/XML/1998/namespace"/>
    <xsd:element name="root" msdata:IsDataSet="true">
      <xsd:complexType>
        <xsd:choice maxOccurs="unbounded">
          <xsd:element name="metadata">
            <xsd:complexType>
              <xsd:sequence>
                <xsd:element name="value" type="xsd:string" minOccurs="0"/>
              </xsd:sequence>
              <xsd:attribute name="name" use="required" type="xsd:string"/>
              <xsd:attribute name="type" type="xsd:string"/>
              <xsd:attribute name="mimetype" type="xsd:string"/>
              <xsd:attribute ref="xml:space"/>
            </xsd:complexType>
          </xsd:element>
          <xsd:element name="assembly">
            <xsd:complexType>
              <xsd:attribute name="alias" type="xsd:string"/>
              <xsd:attribute name="name" type="xsd:string"/>
            </xsd:complexType>
          </xsd:element>
          <xsd:element name="data">
            <xsd:complexType>
              <xsd:sequence>
                <xsd:element name="value" type="xsd:string" minOccurs="0" msdata:Ordinal="1"/>
                <xsd:element name="comment" type="xsd:string" minOccurs="0" msdata:Ordinal="2"/>
              </xsd:sequence>
              <xsd:attribute name="name" type="xsd:string" use="required" msdata:Ordinal="1"/>
              <xsd:attribute name="type" type="xsd:string" msdata:Ordinal="3"/>
              <xsd:attribute name="mimetype" type="xsd:string" msdata:Ordinal="4"/>
              <xsd:attribute ref="xml:space"/>
            </xsd:complexType>
          </xsd:element>
          <xsd:element name="resheader">
            <xsd:complexType>
              <xsd:sequence>
                <xsd:element name="value" type="xsd:string" minOccurs="0" msdata:Ordinal="1"/>
              </xsd:sequence>
              <xsd:attribute name="name" type="xsd:string" use="required"/>
            </xsd:complexType>
          </xsd:element>
        </xsd:choice>
      </xsd:complexType>
    </xsd:element>
  </xsd:schema>
  <resheader name="resmimetype">
    <value>text/microsoft-resx</value>
  </resheader>
  <resheader name="version">
    <value>2.0</value>
  </resheader>
  <resheader name="reader">
    <value>System.Resources.ResXResourceReader, System.Windows.Forms, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</value>
  </resheader>
  <resheader name="writer">
    <value>System.Resources.ResXResourceWriter, System.Windows.Forms, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</value>
  </resheader>
  <data name="action.add" xml:space="preserve">
    <value>Add</value>
  </data>
  <data name="action.addDemoProject" xml:space="preserve">
    <value>Create a demo project</value>
  </data>
  <data name="action.addNewLanguage" xml:space="preserve">
    <value>Add new language</value>
  </data>
</root>
```











