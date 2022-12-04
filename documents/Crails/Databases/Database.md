Interface for database implementations managed by the [Databases] class.

Implementations of this class must provide a static `ClassType` function which returns an [std::string]. The value of that [std::string] must be the same one that's used as parameter for the constructor of the [Database] interface. These values will later be used to ensure that a database handle isn't being casted to the wrong type.
