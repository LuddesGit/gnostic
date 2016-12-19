[![Build Status](https://travis-ci.org/googleapis/openapi-compiler.svg?branch=master)](https://travis-ci.org/googleapis/openapi-compiler)

# OpenAPI Compiler

This repository contains a Go command line tool which reads 
[OpenAPI](https://github.com/OAI/OpenAPI-Specification) 
specifications in JSON or YAML formats and writes
equivalent Protocol Buffer representations. 

[Protocol Buffers](https://developers.google.com/protocol-buffers/)
are a language-neutral, platform-neutral extensible mechanism 
for serializing structured data.

The OpenAPI Compiler reads OpenAPI specifications into 
Protocol Buffer representations and reports errors,
resolves internal dependencies, and writes the results in
in a binary form that can be used in any language that is 
supported by the Protocol Buffer tools.

Code generated by the Protocol Buffer tools includes data
structures with explicit fields for the elements of an OpenAPI
specification. This makes it possible for developers to work
with OpenAPI specifications in type-safe ways. This is 
particularly useful in strongly-typed languages like
Go and Swift.

The OpenAPI Compiler and the OpenAPI Protocol Buffer
representation are automatically generated from the 
[OpenAPI JSON Schema](https://github.com/OAI/OpenAPI-Specification/blob/master/schemas/v2.0/schema.json).
Source code for the generator is in the [generator](generator) directory.

## Disclaimer

This is prerelease software and work in progress. Feedback and
contributions are welcome, but we currently make no guarantees of
function or stability.

## Requirements

OpenAPI Compiler can be run in any environment that supports [Go](http://golang.org)
and the [Google Protocol Buffer Compiler](https://github.com/google/protobuf).

## Installation

1. Get this package by downloading it with `go get`.

        go get github.com/googleapis/openapi-compiler/openapic
  
2. [Optional] Build and run the compiler generator. 
This uses the OpenAPI JSON schema to generate a Protocol Buffer language file 
that describes the OpenAPI specification and a Go-language file of code that 
will read a JSON or YAML OpenAPI representation into the generated protocol 
buffers. Pre-generated versions of these files are in the OpenAPIv2 directory.

        cd $GOPATH/src/github.com/googleapis/openapi-compiler/generator
        go build
        cd ..
        ./generator/generator

3. [Optional] Generate protocol buffer support code. 
A pre-generated version of this file is checked into the OpenAPIv2 directory.
This step requires a local installation of protoc, the Protocol Buffer Compiler.
You can get protoc [here](https://github.com/google/protobuf).

        ./COMPILE-PROTOS.sh

4. [Optional] Rebuild openapi-compiler. This is only necessary if you've performed steps
2 or 3 above.

        go install github.com/googleapis/openapi-compiler/openapic

5. Run the OpenAPI compiler. This will create a file called "petstore.pb" that contains a binary
Protocol Buffer description of a sample API.

        openapic -pb_out petstore.pb examples/petstore.json

6. You can also compile files that you specify with a URL. Here's another way to compile the previous 
example. This time we're creating "petstore.text", which creates a textual representation of the
Protocol Buffer description. This is mainly for use in testing and debugging.

        openapic -text_out petstore.pb.text https://raw.githubusercontent.com/googleapis/openapi-compiler/master/examples/petstore.json

7. For a sample application, see apps/report.

        go install github.com/googleapis/openapi-compiler/apps/report
        report petstore.pb

## Copyright

Copyright 2016, Google Inc.

## License

Released under the Apache 2.0 license.
