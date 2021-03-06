# Optional
### [![Build Status](https://travis-ci.org/DiTo04/optional.svg?branch=master)](https://travis-ci.org/DiTo04/optional) [![Go Report Card](https://goreportcard.com/badge/github.com/DiTo04/optional)](https://goreportcard.com/report/github.com/DiTo04/optional) [![GoDoc](https://godoc.org/github.com/DiTo04/optional?status.svg)](https://godoc.org/github.com/DiTo04/optional)

This is a small library containing the functionality given to Java by `Optional<>`.
It allows Go users to reduce `nil` checks and create more readable code.

## Usage
```go
package example

import opt "github.com/DiTo04/optional"

type Queue interface{
	peekNext() (person opt.Optional)
}

type Person interface{
	GetName() string
}

// Example of Mapping
func getNameOfNext(queue Queue) (str opt.Optional) {
	person := queue.peekNext()
	return person.Map(func(p Person) string {
		return p.GetName()
	})
}

// Example of default values
func getNameOfNextOrGopher(queue Queue) string {
	return getNameOfNext(queue).OrElse("Gopher!").(string)
}

// Example of Filtering
func isFirstPersonGopher(queue Queue) bool {
	return getNameOfNext(queue).Filter(func(s string) bool {
		return s == "Gopher"
	}).OrElse(false).(bool)
}
```

## Inspiration
* [Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)
