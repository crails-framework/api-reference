Libdatatree provides types to dynamically create, walk and edit nested trees of values. [DataTree] and [Data] allow safely walking over nodes, independently of whether they actually exist or not. Each branch can then be converted to arbitrary types (strings, numbers, containers).

Two implementations of libdatatree exist for two targets: native C++ and Cheerp (C++ to JavaScript transpiler).
- The native C++ implementation relies on [boost::property_tree](https://www.boost.org/doc/libs/1_80_0/doc/html/property_tree.html),
- The Cheerp implementation relies on [JavaScript's Object](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Object).
