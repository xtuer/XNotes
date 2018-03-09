```xml
<beans:bean id="springSecurityFilterChain" class="org.springframework.security.web.FilterChainProxy">
    <filter-chain-map request-matcher="ant">
        <filter-chain pattern="/**" filters="
            securityContextPersistenceFilter,
            currentSessionFilter,
            asyncManagerIntegrationFilter,
            logoutFilter,
            usernamePasswordAuthenticationFilter,
            basicAuthenticationFilter,
            requestCacheAwareFilter,
            contextHolderAwareRequestFilter,
            rememberMeAuthenticationFilter,
            anonymousAuthenticationFilter,
            sessionManagementFilter,
            exceptionTranslationFilter,
            filterSecurityInterceptor
        "/>
    </filter-chain-map>
</beans:bean>
```

```json
{
    "1":{},
    "2":{},
    "3":{
        "1": "org.springframework.security.web.context.SecurityContextPersistenceFilter",
        "2": "org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter",
        "3": "org.springframework.security.web.header.HeaderWriterFilter",
        "4": "org.springframework.security.web.authentication.logout.LogoutFilter",
        "5": "org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter",
        "6": "org.springframework.security.web.authentication.www.BasicAuthenticationFilter",
        "7": "org.springframework.security.web.savedrequest.RequestCacheAwareFilter",
        "8": "org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter",
        "9": "org.springframework.security.web.authentication.rememberme.RememberMeAuthenticationFilter",
        "10":"org.springframework.security.web.authentication.AnonymousAuthenticationFilter",
        "11":"org.springframework.security.web.session.SessionManagementFilter",
        "12":"org.springframework.security.web.access.ExceptionTranslationFilter",
        "13":"org.springframework.security.web.access.intercept.FilterSecurityInterceptor"
    }
}
```

**AuthenticationEntryPoint** 是在用户没有登录时用于引导用户进行登录认证的。

## 插入多个 filter

想把多个自定义 filter 插入到某个 filter 前，不能多次使用 before，而是需要使用它们创建一个 CompositeFilter，然后把此 CompositeFilter 使用 before 插入:

```xml
<http auto-config="true" use-expressions="false">
    <intercept-url pattern="/page/admin"   access="ROLE_ADMIN"/>
    <intercept-url pattern="/demo/filters" access="ROLE_USER"/>

    <form-login login-page="/page/login"
                login-processing-url="/login"
                default-target-url="/"
                authentication-failure-url="/page/login?error=1"
                username-parameter="username"
                password-parameter="password"/>
    <logout logout-url="/logout" logout-success-url="/page/login?logout=1"/>
    ...
    <custom-filter ref="authenticationFilters" before="FORM_LOGIN_FILTER"/>
</http>

<!-- Filter 组合 -->
<beans:bean id="authenticationFilters" class="org.springframework.web.filter.CompositeFilter">
    <beans:property name="filters">
        <beans:list>
            <beans:ref bean="oauthAuthenticationFilter"/>
            <beans:ref bean="tokenAuthenticationFilter"/>
        </beans:list>
    </beans:property>
</beans:bean>

<!-- 第三方登陆 filter -->
<beans:bean id="oauthAuthenticationFilter" class="com.xtuer.security.OAuthAuthenticationFilter">
    <beans:property name="authenticationManager" ref="authenticationManager"/>
</beans:bean>
<!-- Token 登陆验证 filter -->
<beans:bean id="tokenAuthenticationFilter" class="com.xtuer.security.TokenAuthenticationFilter">
    <beans:property name="authenticationManager" ref="authenticationManager"/>
</beans:bean>
```



