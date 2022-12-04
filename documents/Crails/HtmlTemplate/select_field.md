Generates a &lt;select&gt; element.

```c++
<%
typedef int OptionType;

std::map<OptionType, std::string> options{
  {0, ""},
  {1, "First option"},
  {2, "Second option"}
};

OptionType selected = 0;
%>

<%= select_field<OptionType>("field-name", options, selected) %> 
```

Generates the following element:

```html
<select name="field-name">
  <option value="=" selected></option>
  <option value="1">First option</option>
  <option value="2">Second option</option>
</select>
```

You may also specify custom attributes using the last optional parameter:

```c++
<%= select_field<OptionType>("field-name", options, selected, {
  {"class", "select-style"}
}) %> 
```
