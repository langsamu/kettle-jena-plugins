# Object-oriented, idiomatic RDF in Java: a manifest-based test suite

This branch shows how to work with in-memory RDF from idiomatic, object-oriented Java. It was made for [The National Archives](https://www.nationalarchives.gov.uk) as a contribution to their [kettle-jena-plugins](https://github.com/nationalarchives/kettle-jena-plugins) project. Pull request: https://github.com/nationalarchives/kettle-jena-plugins/pull/26

## The project at The National Archives
The plugins are part of Project OMEGA at The National Archives. OMEGA replaces the catalogue systems of The National Archives with a single system based on a graph data model. The plugins let data integration pipelines convert records from the existing catalogue databases into RDF with Apache Jena.

## The test suite
The main change is in commit [e25a814](https://github.com/langsamu/kettle-jena-plugins/commit/e25a814d11c6c995bd0cbd8a132c7a0d1fde9ba2). The example is an integration test suite that is described in RDF:
- [`manifest.ttl`](https://github.com/langsamu/kettle-jena-plugins/blob/e25a814d11c6c995bd0cbd8a132c7a0d1fde9ba2/src/test/resources/uk/gov/nationalarchives/pdi/step/jena/manifest.ttl) is an RDF graph. Each entry in it identifies an action to run and the graph that the action must produce.
- Java classes such as [`Manifest`](https://github.com/langsamu/kettle-jena-plugins/blob/e25a814d11c6c995bd0cbd8a132c7a0d1fde9ba2/src/test/java/uk/gov/nationalarchives/pdi/step/jena/Manifest.java) and [`Entry`](https://github.com/langsamu/kettle-jena-plugins/blob/e25a814d11c6c995bd0cbd8a132c7a0d1fde9ba2/src/test/java/uk/gov/nationalarchives/pdi/step/jena/Entry.java) wrap the nodes of that graph. Code uses them as typed objects with properties, and the RDF stays the single source of truth.
- [`TestSuiteIT`](https://github.com/langsamu/kettle-jena-plugins/blob/e25a814d11c6c995bd0cbd8a132c7a0d1fde9ba2/src/test/java/uk/gov/nationalarchives/pdi/step/jena/TestSuiteIT.java) iterates the manifest entries, runs each action and compares the result graph with the expected graph. This replaces the separate per-feature integration tests.

## Similar projects
This approach resulted in these packages:
- JavaScript: https://github.com/rdfjs/wrapper
- .NET: https://github.com/langsamu/dotnetrdf/tree/wrapping/Libraries/dotNetRDF.Wrapping
- Java (work in progress): https://github.com/inrupt/rdf-wrapping-java
