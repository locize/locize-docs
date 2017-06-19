# Getting started

Integrating locize into your website / application takes four steps. If you still got questions after reading the getting started guide - don't hesitate to [contact us](mailto:support@locize.com).

## Step 1) SignUp and create a project

Head over to our app and [register](https://www.locize.io/register). Create your first project by clicking the (+) icon on the dashboard or opening [https://www.locize.io/project/add](https://www.locize.io/project/add) after login.

## Step 2) Decide for a i18n instrumentation

For static websites, smaller webapplications we recommend using our one-liner script locizify. It's the simplest way to get started and needs just a small change of your code:

- **locizify** [learn more](/integration-locizify.md)

For bigger projects or existing projects you like to migrate over to locize you can use:

- **i18next** [learn more](/integration-i18next.md)
- **polyglot** [learn more](/integration-polyglot.md)
- **formatJS / messageformat** [learn more](/integration-formatjs.md)
- **other JSON based frameworks** [learn more](/api.md)
- **other non JSON based** [learn more](/using-with-xliff-gettext.md)



## Step 3) Add new / existing segments

You can add new segments or complete files using the webinterface or the [commandline tool](https://github.com/locize/locize-cli).

![](/assets/addUI.png)

Using locizify or i18next you can enable the saveMissing option - doing so new segments will automatically added to your project.

Using other i18n frameworks you can use the [API](/api.md "API") to do so.

## Step 4) Translate your content

Start translating your content using our Interface or use one of our integrated [3rd party service](/additional-services.md) to order them.