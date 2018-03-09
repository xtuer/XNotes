For reference, `create-session="stateless"` is a better option if you really do have a stateless app such as a RESTful client. This option was introduced in Spring Security 3.1. It will avoid adding parts of Spring Security's infrastructure which make use of the session \(e.g. HttpSessionSecurityContextRepository, SessionManagementFilter, RequestCacheFilter\), so you get a leaner setup.

With `create-session="never"`, Spring Security will never create a session itself, but will make use of one if your app does. In practice, many users aren't even aware that they are creating sessions, **so if you really don't want a session, ever, then stateless is the best option.**

