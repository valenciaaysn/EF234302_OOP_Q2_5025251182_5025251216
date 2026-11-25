# Q051 — Your answer

## (d) HashMap order vs Python dict order

TODO(Q051): explain why printing `map.keySet()` from a `HashMap` may come out in a
different order on another machine or Java version, and what the Python `dict`
guarantees instead (and whether that guarantee is alphabetical).
Java's HashMap does not guarantee the iteration order of its keys. The order depends on the internal hash table arrangement, so it may differ between machines or Java versions.
In contrast, Python's dict guarantees insertion order starting from Python 3.7. This means that keys remain in the order they were first inserted, not in alphabetical order. If alphabetical order is needed, the keys must be sorted explicitly.