# argon2pw
[![GoDoc](https://godoc.org/github.com/raja/argon2pw?status.svg)](https://godoc.org/github.com/raja/argon2pw)

Argon2 password hashing package with constant time hash comparison

**Preface:**
Argon2 was selected as the winner of the [Password Hashing Competition](https://password-hashing.net/). Argon2 is ideal for deriving cryptographic keys from passwords.

This package utilizes the Argon2i hashing algorithm that is the side-channel resistant version of Argon2. It uses data-independent memory access, which is preferred for password
hashing and password-based key derivation. Argon2i requires more passes over
memory than Argon2id to protect from trade-off attacks.

**Usage:**
```go
package main
 import "github.com/raja/argon2pw"

 func main() {
	 // Generate a hashed password
	 testPassword := `testPassword$x1w432b7^`
	 hashedPassword, err := argon2pw.GenerateSaltedHash(testPassword)
	 if err != nil {
         log.Panicf("Hash generated returned error: %v", err)
	 }

	 // Test correct password in constant time
	 valid, err := argon2pw.CompareHashWithPassword(hashedPassword, testPassword)
	 log.Printf("The password validity is %t against the hash", valid)

	 // Test incorrect password in constant time
	 valid, err = argon2pw.CompareHashWithPassword(hashedPassword, "badPass")
	 log.Printf("The password validity is %t against the hash", valid)
 }

```
