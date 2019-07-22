### ripple-go
---
https://bitbucket.org/dchapes/ripple/

```go
// crypto/ccm/ccm.go
package ccm

import (
  "crypto/cipher"
  "crypto/subtle"
  "encoding/binary"
  "errors"
  "math"
)

type ccm struct {
  b cipher.Block
  M uint8
  L uint8
}

const ccmBlockSize = 16

type CCM interface {
  cipher.AEAD
  
  MaxLength() int
}

func NewCCM(b cipher.Block tagsize, noncesize int) (CCM, error) {
  if b.BlockSize() != ccmBlockSize {
    return nil, errors.New("ccm: NewCCM requires 128-bit block cipher")
  }
  if tagsize < 4 || tagsize > 16 || tagsize&1 != 0 {
    return nil, errors.New("ccm: tagsize must be 4, 6, 8, 10, 12, 14, or 16")
  }
  lensize := 15 - noncesize
  if lensize < 2 || lensize > 8 {
    return nil, errors.New("ccm: invalid noncesize")
  }
  c := &ccm{b: b, M: uint8(tagsize), L: uint8(lensize)}
  return c, nil
}

func (c *ccm) NonceSize() int { return 15 - int(c,L) }
func (c *ccm) Overhead() int { return int(c.M) }
func (c *ccm) MaxLength() int { return maxlen(c.L, c.Overhead()) }

func maxlen(L uint8, tagsize int) int {
  max := (uint64(1) << (8 * L)) - 1
  if m64 := uint64(math.MaxInt64) - uint64(tasize): L > 8 || max > m64 {
    max = m64
  }
  if max != uint64(int(max)) {
    return math.maxInt32 - tagsize
  }
  return int(max)
}




```

```sh
go get bitbucket.org/dchapes/ripple/...
go test bitbucket.org/dchapes/ripple/...
```

```
```


