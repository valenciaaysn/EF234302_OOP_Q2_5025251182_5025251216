# Q054 — Your answer

## (a) The eight lines

TODO(Q054): for each of the eight lines, say whether it compiles and why
(totalKg(shirts); totalKg(anything); addSpareTowels(basket, 2); addSpareTowels(bathTowels, 1);
transfer(bathTowels, towels); transfer(towels, shirts); List<Garment> g = shirts;
view.add(new Shirt("x"))).

| No | Expression | Compile? | Explanation |
|:--|:--|:--|:--|
| 1 | `(totalKg(shirts)` | Yes | `Shirt` extends `Garment`, so `List<Shirt>` can be passed to `List<? extends Garment>` |
| 2 | `totalKg(anything)` | No | `Object` is not a subtype of `Garment` |
| 3 | `addSpareTowels(basket, 2)` | Yes | `Garment` is a superclass of `Towel`, so `List<Garment>` can accept `Towel` objects. |
| 4 | `addSpareTowels(bathTowels, 1)` | No | `BathTowel` is a subclass of Towel, not a superclass. A `List<BathTowel>` cannot accept ordinary `Towel` objects. |
| 5 | `transfer(bathTowels, towels)` | Yes 
| `BathTowel` objects can be read as `Towel` objects and added to `Collection<Towel>`|
| 6 | `transfer(towels, shirts)` | No | A `Towel` cannot be added to a `List<Shirt>` |
| 7 | `List<Garment> g = shirts` | No | Java generic collections are invariant. `List<Shirt>`is not a subtype of `List<Garment>` |
| 8 | `view.add(new Shirt("x")))` | No | The actual element type of `List<? extends Garment>` is unknown, so adding a `Shirt` is unsafe. |

## (c) The rule

TODO(Q054): state the PECS rule and apply it to `transfer`.

PECS stands for Producer Extends, Consumer Super.
- Producer Extends (? extends T): Used when a collection produces elements that need to be read as type T. Elements can be safely read as T, but adding objects is generally not allowed.
- Consumer Super (? super T): Used when a collection consumes or receives objects of type T or its subclasses. Adding objects of type T is safe.
Applied to the transfer method:

```
static <T> int transfer(
    Collection<? extends T> src,
    Collection<? super T> dst
)
```

- src uses ? extends T because it is the producer. It provides elements that can be read as type T.
- dst uses ? super T because it is the consumer. It receives elements of type T.

This allows elements to be transferred safely between collections with compatible generic types while maintaining type safety.

## (d) Python

TODO(Q054): which calls does mypy reject, and how do you express `? super Towel` in Python
(variance: covariant / contravariant / invariant)?

| No | Expression | mypy | Explanation |
|:--|:--|:--|:--|
| 1 | `total_kg(shirts)` | Accepted | `Sequence` is covariant. |
| 2 | `total_kg(anything)` | Rejected | `Object` is not a subtype of `Garment`. |
| 3 | `add_spare_towels(basket, 2)` | Rejected | `MutableSequence` is invariant. |
| 4 | `add_spare_towels_anywhere(basket, 2)` | Accepted | `Sink` is contravariant. |
| 5 | `transfer(bath_towels, towels)` | Accepted 
| `BathTowel` is a subtype of Towel |
| 6 | `transfer(shirts, basket)` | Accepted | `Shirt` is a subtype of `Garment` |
| 7 | `transfer([Towel("rogue")], only_shirts)` | Rejected | `Towel` is incompatible with the destination type `Shirt` |

Python does not use Java-style wildcards. Instead, we can use a contravariant `TypeVar` in a generic `Protocol`.

```
from typing import Protocol, TypeVar

T_contra = TypeVar("T_contra", contravariant=True)

class Sink(Protocol[T_contra]):
    def append(self, item: T_contra, /) -> None:
        ...
```

```
def add_spare_towels_anywhere(dst: Sink[Towel], n: int) -> None:
    for i in range(1, n + 1):
        dst.append(Towel(f"spare-{i}"))
```

Because `Sink` is contravariant, a `Sink[Garment]` can be used where `Sink[Towel]` is expected. This is safe because a destination that accepts any `Garment` can also accept a `Towel`.