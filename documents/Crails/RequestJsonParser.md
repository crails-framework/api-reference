Implementation of the [RequestParser] interface that parses a body provided with the `application/json` format and stores it in the [Params] object.

The JSON data is parsed using the [JSON parser from boost property_tree](https://www.boost.org/doc/libs/master/doc/html/property_tree/parsers.html#property_tree.parsers.json_parser).
