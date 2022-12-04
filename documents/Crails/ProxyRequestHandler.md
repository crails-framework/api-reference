Implementation of [RequestHandler] that filters queries matching a set of [ProxyRequestHandler::Rules] and treat them accordingly.

Rules are defined using the `ProxyRequestHandler::rules` global attribute, which you must define when adding the _proxy module_ to your application.
