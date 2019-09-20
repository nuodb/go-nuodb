go-nuodb
========

[NuoDB](http://www.nuodb.com) driver for [Go(golang)](http://www.golang.org) [database/sql](http://golang.org/pkg/database/sql/) interface.

It wraps the libNuoRemote.so C++ API with a custom C API and then uses Cgo for calling it.

## Setup

Installation requires NuoDB in /opt/nuodb and properly set $GOPATH.

```shell
$ go get -d github.com/tilinna/go-nuodb
$ make -C `go env GOPATH`/src/github.com/tilinna/go-nuodb install
```

## Usage

```go
package main

import (
  "database/sql"
	_ "github.com/tilinna/go-nuodb"
)

func main() {
	// func Open(driverName, dataSourceName string) (*DB, error)
	db, err := sql.Open("nuodb", "nuodb://robinh:crossbow@localhost:48004/tests?schema=abcd&timezone=UTC")
}
```

**dataSourceName url string**

Mandatory:

`nuodb://` `username` : `password` @ `broker_address` / `database`

Optional:

* schema=`default schema`
* timezone=`default timezone`
* preferred_address_family=`ipv6`

## Test

### 1. Configure NuoDB

```shell
$ java -jar /opt/nuodb/jar/nuoagent.jar --broker --domain go-nuodb --password archer &
$ /opt/nuodb/bin/nuodb --allow-non-durable --database tests --initialize --password archer --dba-user robinh --dba-password crossbow &
```

### 2. Run the tests

```shell
$ make -C `go env GOPATH`/src/github.com/tilinna/go-nuodb test
```
