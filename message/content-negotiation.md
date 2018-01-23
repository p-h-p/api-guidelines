
# Content Negotiation
Every API **MUST** implement and every API Consumer **MUST** use the [HTTP content negotiation](https://tools.ietf.org/html/rfc7231#section-3.4) where a representation of a resource is requested.

> NOTE: The content negotiation plays the key role in evolving an API, **change management and versioning**.

#### Example
A client is programmed to understand the `application/vnd.example.resource+json; version=2` message format semantics. The client requests a representation of the `/greeting` resource in desired the media type (including its version) from the server:

```
GET /greeting HTTP/1.1
Accept: application/vnd.example.resource+json; version=2
...
```

> NOTE: In the case of technical limitations with semi-colon separated HTTP header values, the semantic version MAY be incorporated in the media type identifier, for example: `application/vnd.example.resource.v2+json` However, the use of semicolon-separated version information is preferred.

The server can provide only a newer version of the requested media type `version=2.1.3`. But since the newer version is backward compatible with the requested `version=2` (related: Changes & Versioning) it can satisfy the request and responds:

```
HTTP/1.1 200 OK
Content-Type: application/vnd.example.resource+json; version=2.1.3
...
```

> NOTE: A server that doesn't have the requested representation media type available MUST respond with the HTTP Status Code **406 Not Acceptable**. 
> 
> NOTE: A server MAY have multiple choices available and MAY respond with the **300 Multiple Choices** response. In which case client SHOULD choose from the presented choices.
> 
> You can read more about content negotiation at [MDN Content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation).
