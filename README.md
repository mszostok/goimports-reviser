<h1 align="center">
  <p>Russian warship, go f*ck yourself!</p>
  <img src="images/warship.jpeg">
</h1>

# goimports-reviser [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Right%20golang%20imports%20sorting%20and%20code%20formatting%20tool%20(goimports%20alternative)&url=https://github.com/incu6us/goimports-reviser&hashtags=golang,code,goimports-reviser,goimports,gofmt,developers)
!['Status Badge'](https://github.com/incu6us/goimports-reviser/workflows/build/badge.svg)
!['Release Badge'](https://github.com/incu6us/goimports-reviser/workflows/release/badge.svg)
!['Quality Badge'](https://goreportcard.com/badge/github.com/incu6us/goimports-reviser)
[![codecov](https://codecov.io/gh/incu6us/goimports-reviser/branch/master/graph/badge.svg)](https://codecov.io/gh/incu6us/goimports-reviser)
![GitHub All Releases](https://img.shields.io/github/downloads/incu6us/goimports-reviser/total?color=green)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/incu6us/goimports-reviser?color=green)
[![goimports-reviser](https://snapcraft.io//goimports-reviser/badge.svg)](https://snapcraft.io/goimports-reviser)
![license](https://img.shields.io/github/license/incu6us/goimports-reviser)
[![Mentioned in Awesome Go](https://awesome.re/mentioned-badge.svg)](https://github.com/avelino/awesome-go) 


!['logo'](./images/reviser-muscot_200.png)


Tool for Golang to sort goimports by 3-4 groups(with own [linter](linter/README.md)): std, general, local(which is optional) and project dependencies.
Also, formatting for your code will be prepared(so, you don't need to use `gofmt` or `goimports` separately). 
Use additional options `-rm-unused` to remove unused imports and `-set-alias` to rewrite import aliases for versioned packages or for packages with additional prefix/suffix(example: `opentracing "github.com/opentracing/opentracing-go"`).
`-local` - will create group for local imports. Values should be comma-separated.


## Configuration:
### Cmd
```bash
goimports-reviser -file-path ./reviser/reviser.go -rm-unused -set-alias -format
```

### Example, to configure it with JetBrains IDEs (via file watcher plugin):
![example](./images/image.png)


### Options:
```text
Usage of goimports-reviser:
  -file-path string
        File path to fix imports(ex.: ./reviser/reviser.go). Required parameter.
  -format
        Option will perform additional formatting. Optional parameter.
  -list-diff
    	Option will list-diff files whose formatting differs from goimports-reviser. Optional parameter.
  -local string
        Local package prefixes which will be placed after 3rd-party group(if defined). Values should be comma-separated. Optional parameters.
  -output string
        Can be "file", "write" or "stdout". Whether to write the formatted content back to the file or to stdout. When "write" together with "-list-diff" will list the file name and write back to the file. Optional parameter. (default "file")
  -project-name string
        Your project name(ex.: github.com/incu6us/goimports-reviser). Optional parameter.
  -rm-unused
        Remove unused imports. Optional parameter.
  -set-alias
        Set alias for versioned package names, like 'github.com/go-pg/pg/v9'. In this case import will be set as 'pg "github.com/go-pg/pg/v9"'. Optional parameter.
  -set-exit-status
    	set the exit status to 1 if a change is needed/made. Optional parameter.

```

## Install
### With Brew
```bash
brew tap incu6us/homebrew-tap
brew install incu6us/homebrew-tap/goimports-reviser
```

### With Snap
```bash
snap install goimports-reviser
```

## Examples
Before usage:
```go
package testdata

import (
	"log"

	"github.com/incu6us/goimports-reviser/testdata/innderpkg"

	"bytes"

	"github.com/pkg/errors"
)
``` 

After usage:
```go
package testdata

import (
	"bytes"
	"log"
	
	"github.com/pkg/errors"
	
	"github.com/incu6us/goimports-reviser/testdata/innderpkg"
)
```

Comments(not Docs) for imports is acceptable. Example:
```go
package testdata

import (
    "fmt" // comments to the package here
)
```  

### Example with `-local`-option

Before usage:

```go
package testdata // goimports-reviser/testdata

import (
	"fmt" //fmt package
	"github.com/pkg/errors" //custom package
	"github.com/incu6us/goimports-reviser/pkg" // this is a local package which is not a part of the project
	"goimports-reviser/pkg"
)
```

After usage:
```go
package testdata // goimports-reviser/testdata

import (
	"fmt" // fmt package

	"github.com/pkg/errors" // custom package

	"github.com/incu6us/goimports-reviser/pkg" // this is a local package which is not a part of the project

	"goimports-reviser/pkg"
)
```

### Example with `-format`-option

Before usage:
```go
package main
func test(){
}
func additionalTest(){
}
```

After usage:
```go
package main

func test(){
}

func additionalTest(){
}
```

---

### If you like the project 

<a href="https://www.buymeacoffee.com/slavka" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;"></a>

### Stargazers

[![Stargazers over time](https://starchart.cc/incu6us/goimports-reviser.svg)](https://starchart.cc/incu6us/goimports-reviser)

