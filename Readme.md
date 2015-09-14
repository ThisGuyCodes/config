Config
=
Configuration management is one of those things that seems simple at first, and (unfortunately) you can get away with *simple* for a while. Until you can't.

Recently (relatively) I've "awakened", as it were, to the more complex (and interesting) aspects of large scale deployment and application management. Concepts like per-service client libraries (as opposed to application libraries), service discovery,  and client-side load balancing. Though many of these sorts of issues have been solved, repeatedly, by many people and companies, there seems to be a distinct lack of high-level abstractions around them (open source at least, and if you have a counter example in Java, I don't care). Even more down to earth things like online configuration changes, or shared secrets, seem a bit disconnected from configuration libraries (that last one is more a personal feeling, I don't too much like the separation between the configuration libraries and management tools, ie: ansible vault).

So, I feel like a lot of these sort of things could be handled for the developers. Yes all the pieces to create this exist, but each team/company/project shouldn't have to assemble all the pieces themselves. We're better than that. We can create a better, DRY'er, more fluid developer experience around this problem set.

An Experiment
-
So I want to make solving these problems trivial. A default even. The aim of this project is to provide a library for seamlessly handling as many of these sorts of problems as possible, as well as a set of conventions to help developers understand how to make their applications easily changeable (in particular, how to handle/allow online config changes comes to mind). This is meant to serve as an experimentation ground, as well as an example for developers and other libraries; **however**, it first and foremost must be *useful* in itself.

Something I really want to emphasise here is a focus on the *developer experience*. Good defaults, reduced boilerplate, clear communication of behavior, etc. Basically, "feels clunky" is our worst enemy.

Goals
-
More specifically, I want these things:

* [ ] Tool to generate statically-typed representation of a config file
* [ ] Support many formats (json, yaml, xml, *protobuf*)
	* [ ] Intermixing of formats (define fields with protobuf, type config with yaml)
* [ ] Configuration inheritance
	* [ ] Checks around config values (ie: field exists in stage but not prod)
* [ ] Easy integration with "change methods" (ways to update the config). Should also ship with integrated defaults:
	* [ ] Config stores (etcd, consul, ...)
		* [ ] Include API key retrieval/input
	* [ ] File watching
	* [ ] Provide integrated way to "wait" for configuration changes, for when custom change handling is necessary
* [ ] Native support for service discovery
	* [ ] DNS
		* [ ] Include full implementation of SRV records
	* [ ] HTTP api (etc, consul, even riak's http api)
	* [ ] Pluggable interface for other sources
	* [ ] Include support for weights (aka client-side load balancing), ie: SRV records.
* [ ] Secret management
	* [ ] Decrypt into memory, leave encrypted on disk
		* [ ] Support getting decryption key from a variety of sources
		* [ ] Tooling to make inspecting encrypted contents simple
	* [ ] Encrypted values in otherwise unencrypted config
	* [ ] Secondary/separate config store for secrets (references)

As it stands (just thinking about it). This will involve both a tool to generate a statically-typed representation of a config, and a supporting library (to handle everything else).

Wish me luck.
