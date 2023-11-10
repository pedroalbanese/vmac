# VMAC
[![ISC License](http://img.shields.io/badge/license-ISC-blue.svg)](https://github.com/pedroalbanese/vmac/blob/master/LICENSE.md) 
[![GoDoc](https://godoc.org/github.com/pedroalbanese/vmac?status.png)](http://godoc.org/github.com/pedroalbanese/vmac)
[![Go Report Card](https://goreportcard.com/badge/github.com/pedroalbanese/vmac)](https://goreportcard.com/report/github.com/pedroalbanese/vmac)

### Variable Message Authentication Code
VMAC stands for "Variable Message Authentication Code." It is a method for generating a message authentication code, a type of cryptographic checksum, that ensures the integrity and authenticity of a message. VMAC is designed to provide security against various cryptographic attacks while offering high performance. It uses a block cipher to process variable-length messages and produce a fixed-size authentication tag. This tag can be used to verify that the message has not been altered and comes from a legitimate sender.
## Example
```go
package main

import (
	"crypto/aes"
	"fmt"
	"log"

	"github.com/pedroalbanese/vmac"
)

func main() {
	// Example using the AES block cipher
	key := []byte("0000000000000000")
	nonce := []byte("00000000000000")
	message := []byte("The quick brown fox jumps over the lazy dog.")

	block, err := aes.NewCipher(key)
	if err != nil {
		log.Fatal(err)
	}

	// Create a new VMAC using the AES block cipher
	mac, err := vmac.New(block, key, nonce, 16) // 16 is the VMAC size in bits
	if err != nil {
		log.Fatal(err)
	}

	// Write the message to the VMAC
	_, _ = mac.Write(message)

	// Calculate the VMAC
	calculatedVMAC := mac.Sum()

	// Display the calculated VMAC
	fmt.Printf("VMAC: %x\n", calculatedVMAC)
}
```

Shamelessly taken from:  
https://github.com/nicksnyder/vmac.go
