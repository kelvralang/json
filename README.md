# moglang/json

Canonical import: `github.com/moglang/json`.

JSON is represented by a recursive `Json` DOM, not heterogeneous MOG
collections. Arrays are `Array<Json>` and objects are `Dict<str, Json>`, so
MOG’s normal collection type guarantees remain intact. Parsed values expose
`kind`, `boolean`, `number`, `text`, `items`, and `fields`.

```mog
const json = @import("github.com/moglang/json")
var document json.Json = json.parse("[1,true,null]")
print(json.stringify(document))
```

The parser accepts JSON strings, numbers, booleans, nulls, arrays, and objects;
serialization emits deterministic object-key order. Unicode `\uXXXX` escapes,
including valid surrogate pairs, are decoded to UTF-8.
