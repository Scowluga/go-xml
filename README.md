[![GoDoc](https://godoc.org/aqwari.net/xml?status.svg)](https://godoc.org/aqwari.net/xml) [![Build Status](https://travis-ci.org/droyo/go-xml.svg?branch=master)](https://travis-ci.org/droyo/go-xml)

# Installation

Requires go 1.9 or greater for golang.org/x/html dependency.

```
go get aqwari.net/xml/...
```

This repository contains a collection of Go packages for working
with XML, with the ultimate goal of enabling code generation based
on XML documents.

- The `xmltree` package converts xml documents to a tree data
  structure, and provides convenient methods for manipulating and
  searching through that tree.
- The `xsd` package implements a parser for XML Schema. It takes
  some liberties from the specification, and would need some work for
  use as a validator, but it handles type inheritance and XML namespaces
  in a relatively sane way.
- The `xsdgen` package provides a customizable code generator that
  generates Go type declarations and marshal/unmarshal methods for
  an XML Schema.
- The `wsdl` package parses Web Service Definition Language (WSDL)
  files, which describe a (usually) SOAP web service.
- The `wsdlgen` package generates Go source code from WSDL files.
- The `xsdgen` and `wsdlgen` commands generate Go code with default
  settings and are suitable for use with `go generate`.

The directory wsdlgen/examples contains packages that were (mostly)
automatically generated using the wsdlgen package. You can run

	go generate

within the subdirectories to re-generate the code if you make changes
to the wsdlgen package.
This code is still very rough around the edges, but I have succesfully
used it to generate type declarations for some pretty complex XML
schema from an Apache Axis application. There are github issues
opened for missing functionality.

# Fork Changes

The purpose of this fork is to automate (as much as possible) the process of generating Golang source code from the MusicXML XSD. 
This is to support the [go-musicxml library](https://github.com/alda-lang/go-musicxml). 
Here are the changes made so far: 

- Added a copy of the [musicxml.xsd](https://github.com/w3c/musicxml/blob/v3.1/schema/musicxml.xsd). Updated the file to have a namespace, so it works with code generation. 
- Removed the added namespace in the generated `xml:` struct tags.
- Updated name generation to make MusicXML types and names MixedCaps. 
- Updated type generation to generate pointers. This is so optional parameters can be `nil`. Currently, only complex types are pointers, although this is likely to change.   