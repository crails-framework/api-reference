Replaces all occurence of a pattern found within a [std::string]. The pattern can be expressed either as a [std::string_view] or a [std::regex]. The replacement can be expressed through a [std::string_view], or may be generated dynamically using a lambda.

# Examples

Replacing a simple pattern with a string:

```c++
std::string cats("cats are catstastic");
std::string dogs = Crails::replace_all_occurences(cats, "cat", "dog");

cout << dogs << endl; // prints: "dogs are dogstastic";
```

Replacing regex matches with a string:

```c++
std::string confidential("The password is <PASSWORD>secret</password>");
std::regex  password_pattern("<password>[^<]*</password>", regex_constants::icase);

// prints "The password is ****"
cout << Crails::replace_all_occurences(confidential, password_pattern, "****") << endl;
```

Repalcing regex matches with dynamically generated fillings:

```c++
std::string html("Hello [b]world[/b] !");
std::regex  pattern("\\[b][^[]*\\[/b]"),

html = Crails::replace_all_occurences(html, pattern, [](const std::string_view match) -> std::string
{
  string content(match.substr(3, match.length() - 7));
  return "<strong>" + content + "</strong>";
});
cout << html << endl; // prints "Hello <strong>world</world> !"
```
