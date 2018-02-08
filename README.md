# azure-chaos-frontend

web frontend for [azure-chaos](https://github.com/bengreenier/azure-chaos). :cloud:

This simply surfaces the `azchaos` functionality via authenticated API.
By default, this runs on port `3000` - but that can be configured with the `PORT` environment variable.

To configure this authentication layer, use the following environment variables:

+ `AUTH_CLIENT_ID` - an AzureAD application client id
+ `AUTH_ISSUER` - the AzureAD issuer
+ `AUTH_AUDIENCE` - the AzureAD audience

See [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad#5212-options) for more details.

## API

> All endpoints require `Authentication: Bearer <token>` header authentication values for the configured AzureAD application.

### GET /extensions

Returns all registered extensions, as an array:

```
[
    {
        "name": "test",
        "desc": "test desc",
        "uri": "https://test.com"
    }
]
```

### POST /extensions

Creates a new extension. Takes `name, uri, desc` as parts of a json payload.

### GET /extensions/:extId

Gets a particular extension. Takes `extId` (the name of the extension) as part of the path.

```
{
    "name": "test",
    "desc": "test desc",
    "uri": "https://test.com"
}
```

### POST /extensions/:extId/start

Starts an extension. Takes `extId` (the name of the extension) as part of the path.
Optionally takes `?code=<value>` as a query parameter, where `code` is passed along
to the extension. Takes `accessToken` and `resources` as parts of a json payload.

### POST /extensions/:extId/stop

Stops an extension. Takes `extId` (the name of the extension) as part of the path.
Optionally takes `?code=<value>` as a query parameter, where `code` is passed along
to the extension. Takes `accessToken` and `resources` as parts of a json payload.

### DELETE /extensions/:extId

Deletes an extension. Takes `extId` (the name of the extension) as part of the path.

## License

MIT