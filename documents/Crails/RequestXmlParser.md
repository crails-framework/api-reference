Implementation of the [RequestParser] interface that parses a body provided with the `application/xml` or `text/xml` format, and stores it in the [Params] object.

The XML data is parsed using the [XML parser from boost property_tree](https://www.boost.org/doc/libs/master/doc/html/property_tree/parsers.html#property_tree.parsers.xml_parser).
