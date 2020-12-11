# Notes on SpiderMonkey

JS::Context -> Represents the execution of JS code, there may be multiple per thread.


| From        | Relationship | To              | Notes |
| ----------- | ------------ | --------------- | ----- |
| Thread      | One to many  | JS::Context     |
| JS::Context | One to one   | JS::Compartment |  |
| JS::Context | One to many  | JS::Realm       | JS::Compartment->realms_ (vector) |

# Thread
 * Contains 1 `JS::Context`
 * Contains many `JS::Realm`
 * Contains many `JS::Compartment`

# `JS::Context`
 * Represents a thread, contains all thread local state
 * Is associated with one compartment at a time

# `JS::Compartment`
 * Remembers all its realms `JS::Compartment->realms_` (vector)
 * Represents a security boundary that JS things run and live in.
 * Has one parent `JS::Zone`, which is a GC boundary. Some memory may be shared between compartments.

# `JS::Realm`
 * References 1 `JSRuntime`
 * References 1 `JS::Zone`

The realm is set here:
https://searchfox.org/mozilla-central/rev/444ee13e14fe30451651c0f62b3979c76766ada4/js/src/vm/JSContext-inl.h#422
