Useful conversations where stacks would be helpful:
https://bugzilla.mozilla.org/show_bug.cgi?id=1530430#c19

---

Script to get DMD reports out of android:
https://github.com/mozilla-b2g/B2G/blob/master/tools/get_about_memory.py

Stack walking in counters are here:
https://searchfox.org/mozilla-central/rev/f91bd38732d4a330eba4e780812274b98eb81274/tools/profiler/core/memory_hooks.cpp#70

Don't re-enter here
https://searchfox.org/mozilla-central/rev/f91bd38732d4a330eba4e780812274b98eb81274/tools/profiler/core/memory_hooks.cpp#97

Need a separate check for each arena.

Boolean is associated with the arena that has the lock.

`replace_malloc` - one static bool flag

`replace_moz_arena_malloc`

Follow-up with glandium. He is Mr. jemalloc();

https://searchfox.org/mozilla-central/rev/f91bd38732d4a330eba4e780812274b98eb81274/memory/build/mozjemalloc.cpp#1055

"How do I get access to the arenas from the hook?"

jeMallocTable - expose a getter and setter method,
(arena_id_t) => bool
(arena_id_t, bool) => void

jseward - lul

---

DMD

AllocCallback
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/DMD.cpp#1058

InfallibleAllocPolicy
Gives you access to the underlying malloc functions
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/DMD.cpp#101

Here is an example of using "new" with this policy:=
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/DMD.cpp#1387

Re-entry handling:
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/DMD.cpp#1112

Does DMD handle arenas

Analyze the live heap, and serialize it out to a json file
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/DMD.cpp#1619
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/DMD.h#136

Like a million allocations, first 2 seconds
Full trace is probably bonkerballs

Post processing happens here:
https://searchfox.org/mozilla-central/rev/8a990595ce6d5ed07ace2d4d5d86cc69aec90bde/memory/replace/dmd/dmd.py
