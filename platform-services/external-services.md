# External Services

Game servers can make web requests to external API's using the built-in `HttpManager`. Each request is signed and can be validated by the service you are calling, see [#verifying-gameserver-http-requests](external-services.md#verifying-gameserver-http-requests "mention") below.

## Overview

```typescript
// Web Requests can only be made on the gameservers. Requests made on the client will fail.
if (!Game.IsServer()) return;

let getResult = HttpManager.GetAsync("https://jsonplaceholder.typicode.com/todos/1");
print(getResult.statusCode, getResult.data);

let postResult = HttpManager.PostAsync("https://jsonplaceholder.typicode.com/posts", json.encode({
	title: 'foo',
	body: 'bar',
}));
print(postResult.statusCode, postResult.data);


```

### Supported Methods

```typescript
GetAsync(url: string, headers: string): HttpResponse;
GetAsync(url: string): HttpResponse;
PatchAsync(url: string, data: string): HttpResponse;
PatchAsync(url: string, data: string, headers: string): HttpResponse;
PostAsync(url: string, data: string): HttpResponse;
PostAsync(url: string, data: string, headers: string): HttpResponse;
PutAsync(url: string, data: string): HttpResponse;
PutAsync(url: string, data: string, headers: string): HttpResponse;
PutAsync(options: RequestHelper, headers: string): HttpResponse;
DeleteAsync(url: string): HttpResponse;
DeleteAsync(url: string, headers: string): HttpResponse;
```

### Verifying GameServer HTTP Requests

Requests originating from a GameServer will include an additional header called: `x-airship-signature` containing a JWT with request details including:

```typescript
{
  "jti": string, // JWT ID - UUID e.x. 8e2b6b98-14ba-4724-b95b-3627b6d48d5b
  "iat": number, // u64 - Timestamp this jwt was issued, in seconds since Unix Epoch
  "exp": number, // u64 - Timestamp this jwt expires, in seconds since Unix Epoch
  "hostname": string, // e.x. "mywebsite.test" Will include port if not https, http 443, 80
  "path": string, // e.x. "/path/123" excludes query params
  "method": string, // GET, POST, etc.
  "gameId": string, // This should match your gameId on create.airship.gg
  "serverId": string,
  "sceneId": string, // The default starting scene of the server (doesn't update if changed)
  "region": string,
  "organizationId": string,
  "type": "game-server"
}
```

Each JWT is signed with a specific public key that can be identified in the header using `kid`:

```json
{
  "typ": "JWT",
  "alg": "ES256",
  "kid": "f24d25f2-e49b-424b-8e61-cf9c8219b332"
}
```

Using the `kid` you can validate the JWT against Airship public keys using our JWKS endpoint: [https://airship.gg/.well-known/jwks.json](https://airship.gg/.well-known/jwks.json)

Read more here: [https://stytch.com/blog/understanding-jwks/](https://stytch.com/blog/understanding-jwks/)

Examples verifying a JWT using JWKS can be found here: [https://github.com/panva/jose/blob/main/docs/jwks/remote/functions/createRemoteJWKSet.md](https://github.com/panva/jose/blob/main/docs/jwks/remote/functions/createRemoteJWKSet.md)

When validating the token, ensure the JWT is signed by an Airship public key and ensure the hostname / path matches your API url.
