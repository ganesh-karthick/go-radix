go-radix [![Build Status](https://travis-ci.org/ganesh-karthick/go-radix.svg?branch=master)](https://travis-ci.org/ganesh-karthick/go-radix)
=========

Provides the `radix` package that implements a [radix tree](http://en.wikipedia.org/wiki/Radix_tree).
The package provides a non thread safe `Tree` based on [armon/go-radix](https://github.com/armon/go-radix)
and a  thread Safe ``ConcurrentTree`` implementation on top of it, optimized for sparse nodes.

As a radix tree, it provides the following:
 * O(k) operations. In many cases, this can be faster than a hash table since
   the hash function is an O(k) operation, and hash tables have very poor cache locality.
 * Minimum / Maximum value lookups
 * Ordered iteration

For an immutable variant, see [go-immutable-radix](https://github.com/hashicorp/go-immutable-radix).

Documentation
=============

The full documentation is available on [Godoc](http://godoc.org/github.com/ganesh-karthick/go-radix).

Example
=======

Below is a simple example of usage

```go
// Create a tree
r := radix.New()
r.Insert("foo", 1)
r.Insert("bar", 2)
r.Insert("foobar", 2)

// Find the longest prefix match
m, _, _ := r.LongestPrefix("foozip")
if m != "foo" {
    panic("should be foo")
}
```

Below is a simple example of Thread Safe usage

```go
// Create a Concurrent tree
r := radix.NewConurrentTree()
r.Insert("foo", 1)
r.Insert("bar", 2)
r.Insert("foobar", 2)
r.Delete("bar")

// Find the longest prefix match
m, _, _ := r.LongestPrefix("foozip")
if m != "foo" {
    panic("should be foo")
}
```
