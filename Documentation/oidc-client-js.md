# Connect oidc-client-js with dex

[oidc-client-js](https://github.com/IdentityModel/oidc-client-js) is a library to provide OpenID Connect 
support for client-side browser based Javascript client applications.
Wrappers or examples exists to use it within [Angular2](https://github.com/jmurphzyo/Angular2OidcClient) or 
[ReactJS/Redux](https://github.com/maxmantz/redux-oidc) applications.

## dex configuration for the implicit flow
The following configuration is required for dex:
```
oauth2:
  responseTypes:
  - 'id_token'
  - 'token'                  # by default, dex allows only the 'code' response type

web:
  allowedOrigins:
  - '*'                      # or your domain name 'client.example.com'
```

## oidc-client-js configuration
The following configuration is to be set for the UserManager:
```
 var settings = {
    authority: 'http://127.0.0.1:5556/dex',
    client_id: 'example-app',
    redirect_uri:'http://127.0.0.1:3000/callback.html',
    response_type: 'id_token token',
    scope: 'openid email',

    loadUserInfo: false
};
```

Do not forget to register your `client_id` within dex and to properly setup the code to handle the callback.


## Known limitations
The following features are implemented within the client but not yet supported by dex:
- user info endpoint (use `loadUserInfo: false` in your settings)
- logout
