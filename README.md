# Kroxylicous

## What?

Kroxylicious is a project aiming to provide an open source pluggable framework for writing network proxies that understand the Apache Kafka protocol.

## Why?

Proxies are a powerful architectural pattern which are widely used for other application-layer protocols, such as HTTP.

They _could_ solve a number of problems organizations have using Kafka. 
While some organizations running Apache Kafka have written Kafka-aware proxies, they have tended to remain closed-source and do very specific things.

Kroxylicious is an early-stage project which seeks to lower the cost of developing Kafka proxies by providing a lot of the common requirements out-of-the-box.

This lets developers focus on the logic needed to get _their_ proxy to do what _they_ need.

## How?

Kroxylicious provides a network layer (built on Netty) and leverages the KRPC deserialization and serialization code from Apache Kafka to provide a configurable and pluggable abstraction for inspecting and modifying requests and responses.
This abstraction is known as a _protocol filter_. Protocol filters can be combined in a sequence (i.e. the filter chain pattern).
The APIs are designed so that filters _compose_, working together without needing to know what other filters exist in the chain.

For example:

* Alice might write a filter that validates that records in `Produce` requests conform to a topic-specific schema, rejecting those which do not.
* Bob might write a filter which encrypts records within `Produce` requests and decrypts records within `Fetch` responses in order to guarantee encryption at rest. 
* Carol might configure her proxy to use both these filters so that records are both schema validated and encrypted.

The API that Alice and Bob use to write their filters is:

* A Java API
* type safe
* abstracted from the networking layer (Netty is an implementation detail from their point of view)

They just have to focus on the logic needed for their filter, using their knowledge of the Kafka protocol.

## So what?

If this seems interesting to you please join in on GitHub.

## Organisation

Take a look at the following resources to learn more about the current state of discussions, thinking and first PoC:

* [Our GitHub Org](https://github.com/kroxylicious): Kroxylicious Organisation
* [Kproxy](https://github.com/kroxylicous/kproxy): A basic PoC for a Kafka protocol proxy based on Netty
* [Design](https://github.com/kroxylicious/design): Design thoughts & concepts
* [Discussions](https://github.com/kroxylicous/design/discussions): Ideas and other discussions
* [Resources](https://github.com/kroxylicious/design/blob/main/useful-resources.asciidoc): A collection of useful resources
* [License](https://github.com/kroxylicious/kproxy/blob/main/LICENSE): This code base is available under the Apache License, version 2
