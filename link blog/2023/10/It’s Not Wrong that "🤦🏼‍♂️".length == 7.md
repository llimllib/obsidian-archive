---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://hsivonen.fi/string-length

> But It’s Better that "🤦🏼‍♂️".len() == 17 and Rather Useless that len("🤦🏼‍♂️") == 5

After reading this article, I [wanted to see](https://hachyderm.io/@llimllib/110472085644702768) how go handled the titular question:

```go
package main

import (
	"fmt"
	"unicode/utf8"

	"github.com/rivo/uniseg"
)

var s = "🤦🏼‍♂️"

func main() {
	fmt.Printf("length of string %s with various tools\n\n, s)
	fmt.Printf("len():                            %d\n", len(s))
	fmt.Printf("utf8.runeCountInString:           %d\n", utf8.RuneCountInString(s))
	fmt.Printf("len([]rune()):                    %d\n", len([]rune(s)))
	fmt.Printf("rivo/uniseg.GraphemeClusterCount: %d\n", uniseg.GraphemeClusterCount(s))
}
```

```console
$ ./runetest
length of string 🤦🏼‍♂️ with various tools

len():                            17
utf8.runeCountInString:           5
len([]rune()):                    5
rivo/uniseg.GraphemeClusterCount: 1
```

[akkartik kindly pointed me](https://hachyderm.io/@akkartik@merveilles.town/110472179616674843) to [libgrapheme](https://libs.suckless.org/libgrapheme), which looks cool.