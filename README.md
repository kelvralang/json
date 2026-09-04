# kelvralang/json

JSON parsing, validation, and deterministic serialization for Kelvra.

## Install and import

```sh
kelvra add github.com/kelvralang/json@v0.2.0
```

JSON is represented by a recursive `Json` DOM, not heterogeneous KELVRA
collections. Arrays are `Array<Json>` and objects are `Dict<str, Json>`, so
KELVRA’s normal collection type guarantees remain intact. Parsed values expose
`kind`, `boolean`, `number`, `text`, `items`, and `fields`.

```kelvra
const json = @import("github.com/kelvralang/json")
var document json.Json = json.parse("[1,true,null]")
print(json.stringify(document))
```

Prefer the checked constructors and accessors when creating or reading values:

```kelvra
var items Array<json.Json> = []
items.push(json.stringValue("Kelvra"))
items.push(json.numberValue(2.0))

var document json.Json = json.arrayValue(items)
print(json.kindOf(document))
print(json.asString(json.asArray(document)[0]))
```

The canonical import is `github.com/kelvralang/json`; `package.api.kel` is the
complete public contract.

## Behavior and errors

The parser accepts JSON strings, numbers, booleans, nulls, arrays, and objects;
serialization emits deterministic object-key order. Unicode `\uXXXX` escapes,
including valid surrogate pairs, are decoded to UTF-8.

Parsing rejects malformed escapes, numbers, surrogates, delimiters, and trailing
input with a runtime error. Duplicate object keys are accepted with the last
value winning. `numberValue` and `stringify` reject NaN and positive or negative
infinity because JSON has no representation for them. Accessors raise a runtime
error when the value has the wrong kind.

`Json` fields remain public for compatibility. Direct mutation can create an
invalid DOM, so constructors are recommended for new code.
`kindOf` returns one of `"null"`, `"bool"`, `"number"`, `"string"`, `"array"`,
or `"object"`.

`tests/main.kel` covers successful parsing and construction. Programs under
`tests/errors/` are negative fixtures and pass when the interpreter rejects
them.

## Compatibility

Version 0.2.0 requires Kelvra runtime `^0.2.0`. This source package has no native
build or operating-system dependency. Parsing state is local to each `parse`
call; the package does not retain document input globally. It is licensed under
GPL-3.0-only; see `LICENSE`.
