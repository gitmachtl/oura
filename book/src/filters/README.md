# Filters

_Filters_ are intermediate steps in the pipeline that process events as they travel from _sources_ to _sinks_. They might serve different pourposes, such as: selecting relevant events, enriching event data, transforming data representation, etc.

## Built-in Filters

These are the existing filters that are included as part the main _Oura_ codebase:

- [Fingerprint](fingerprint.md): a filter that adds a (probably) unique identifier (fingerprint) to each event.
- [Selection](selection.md): a filter that evaluates different built-in predicates to decide which events should go through the pipeline.

New filters are being developed, information will be added in this documentation to reflect the updated list. Contributions and feature request are welcome in our [Github Repo](https://github.com/txpipe/oura).
