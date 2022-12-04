Represents the transient state of an HTTP repsonse that may be sent to a client at any moment. It wraps a [HttpResponse] object, and can progressively edit it until the `send` method gets called.

After calling the `send` method, any changes applied on the BuildingResponse won't reach the client anymore.
