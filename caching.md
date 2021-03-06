# What is Cache-Control max-age?
The Cache-Control max-age defines the amount of time a file should be cached for.

The max-age response directive indicates that the response is to be considered stale after its age is greater than the specified number of seconds.

The max-age is expressed in seconds.

Common max-age values are:

- Disabled cache: max-age=0
- Five seconds: max-age=5
- One minute: max-age=60
- One hour: max-age=3600
- One day: max-age=86400
- One week: max-age=604800

When using max-age to define your cache times one should consider how fast your users should be able to request the updated files.

For example for versions used by the development teams we recommend to disable the cache functionality.

For production versions we recommend a low cache value.

![](/assets/app-settings.png)

**Remember: if you for example have a max-age of 604800 your users could have to wait up to one week before receiving the updated file.**

