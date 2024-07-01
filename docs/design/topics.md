# Topics

Authors: [Philip Metzger](mailto:philipmetzger@bluewin.ch), [Noah Mayr](mailto:dev@noahmayr.com)
 [Anton Bulakh](mailto:him@necaq.ua)

## Summary

Introduce Topics as a truly Jujutsu native way for topological branches, which 
also replace the current bookmark concept for Git interop. As they have been
documented to be confusing users coming from Git. They also replace the 
`[experimental-advance-branches]` config for those who currently use it, as 
such a behavior will be built-in for Topics.

## Prior work 

Currently there only is Mercurial which has a implementation of 
[Topics][hg-topic]. There also is the [Topic feature][gerrit-topics] in Gerrit,
which groups commits with a single identifier.


## Goals and non-goals

### Goals

The goals for this Project are small, see below.

* Introduce the concept of topological branches for Jujutsu.
* Simplify Git interop by reducing the burden on `jj bookmark`.
* Add Change metadata as a concept.
* Remove the awkward `bookmark` to Git `branch` mapping.

### Non-Goals

## Overview

A detailed overview of the project and the improvements it brings.

### Detailed Design


#### Storage

We should store `Topic` metadata as pure commit metadata in the serialized proto:


```protobuf
message Commit {
  //...
  map<string, string> topics = N;
}
```

while the actual code should look like this:

```rust
#[derive(ContentHash, ...)]
struct Commit {
  //...
  #[ContentHash(ignore = true)]
  topics: HashMap<String, String>
}
```

#### Backend implications

If Topics were stored as commit metadata, it would allow backends to drop 
the metadata if necessary. 

TODO: Write it

## Alternatives considered 


### Store them not on the Commit

See [#1889][prototype] for another idea of keeping the  

Other alternatives to your suggested approach, and why they fall short.

### Single Head Topics

While these are conceptually simpler, they wouldn't help with ...

## Future Possibilities

The section for things which could be added to it or deemed out of scope during
the discussion.

[hg-topics]:
[gerrit-topics]: 
