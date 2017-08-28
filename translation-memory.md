# Smart translation memory

In contrast to traditional translation memories the implementation inside locize brings following benefits:

- better performance - the translation memory runs directly in your browser and provides faster results by not having to roundtrip to the server
- the translation memory can be configured to use multiple projects - so you can reuse translations from all your existing projects
- the translation management search works not only on exact language pairs but also shows results for languages of the same family, eg. en-GB results while you search in en-US
- you can use the fuzzy search to lookup lexical terminology and check for consistent usage of terminology
- every result has a link back to it's source project which makes maintaining the memory and keeping translation consistency a breeze

# Configuration of the translation memory

You can configure your translation management from the settings page - services. On new projects the service is enabled by default and the project itself is selected as translation memory source.

In the settings you can:

- enable / disable the service
- add / remove projects which should be used as translation memory source

<img src="/assets/img/translationmemory.png" width="80%" />


# reload the translation memory

The translation memory will be loaded on startup an will be cached for 24h in your browsers indexeddb.

If there were a lot of changes and you like to reload your cache you can use the reload translation memory button from your project overview:

<img src="/assets/img/translationmemory_reload.png" width="80%" />




# Using the translation memory

When enabled you will see a "TM Lookup" button on every segment (bottom center). Clicking it will enable a translation memory lookup for this segments.

<img src="/assets/img/translationmemory_consistency.png" width="80%" />



On every match you will find:

- TM score (the smaller the better the match)
- Link to the source of this translation
- Source language text
- Target language translation
- Button to accept the translation memory entry

## Lexical lookup / consistency

In the translation memory search field you can enter any text you like. This way you can easily lookup single words and check if the translations use the same terminology all over the places.

<img src="/assets/img/translationmemory_consistency.png" width="80%" />


Compare the translation for intership in german - once translated as "praktika" and another time as "praktikum". Just follow the link to source and fix that inconsistency.

