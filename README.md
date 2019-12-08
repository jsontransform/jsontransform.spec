# jsontransform

## structure

A `jsontransform` document is a [https://json.org/](JSON) document.
At its uppermost level it consists of an object with the following
required and optional keys:

* **`version`** *(required, string)* The version of `jsontransform` which is used
  in this document. According to this specification only one version is recognized:
  `"2020-01-01"`.
* **`templates`** *(optional, array)* An array of *template* objects.
* **`functions`** *(optional, object)* An object that maps function names to
  *function definition* objects.
* **`patterns`** *(optional, object)* An object that maps pattern names to
  *match definition* objects.

## paths

A json path selects a piece of a json document. A json path follows the following
production rule:

    jsonpath := propertyselector ("." propertyselector)*
    propertyselector := fieldselector indexselector*
    indexselector := "[" (quotedselector | numberselector) "]"
    fieldselector := quotedselector | literalselector
    quotedselector := "'" ([^'] | "''")+ "'"
    literalselector := [a-zA-Z_-][a-zA-Z0-9_-]*
    numberselector := [0-9]+

Example paths:

    foo
    foo.bar
    foo['bar']
    foo['bar'].qux
    foo['bar'].'qux'
    'foo'['bar'].qux
    'foo'['bar'].'qux'
    foo['bar']['qux']
    foo.bar[0]
    foo.bar[0][1]
    foo.bar.'0'.'1'
    'foo'.bar
    'foo'.'bar'
    foo['bar']

## regular expressions

A *regular expression* 

## match definitions

A *match definition* is a piece of json. If it is either of the following
it matches the given value as is:

* a string (e.g. `"foo"`)
* a number (e.g. `3` or `-3.4`)
* a boolean (i.e. `true` or `false`)
* `null`

If a match definition object is an actual json object it matches each key/value
pair. Each key specifies a *path* in the json document to be matched.

## function definitions

A function can be thought of as a named template that takes named arguments.

