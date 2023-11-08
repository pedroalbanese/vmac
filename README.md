# vmac
### VMAC: Message Authentication Code using Universal Hashing

## Example
```go
package main

import (
	"crypto/aes"
	"encoding/hex"
	"fmt"
	"log"

	"github.com/pedroalbanese/vmac"
)

func main() {
	// Example using the AES block cipher
	key, _ := hex.DecodeString("00000000000000000000000000000000")
	nonce, _ := hex.DecodeString("00000000000000000000000000000000")
	message := []byte("Yoda said, do or do not. There is no try.")

	block, err := aes.NewCipher(key)
	if err != nil {
		log.Fatal(err)
	}

	// Create a new VMAC using the AES block cipher
	mac, err := vmac.New(block, nonce, message, 64) // 64 is the GMAC size in bits
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
