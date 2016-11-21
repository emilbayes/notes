Lately I've been toying with the idea of generating public/private keys from passpharses to make it easy to bring your keys with you. I've tried to find all the security concerns I could on the subject, but I'm hoping more people here can help point out issues that would need to be taken care of for this to be a viable idea. The below might be a bit messy as I have some very concrete use-cases in mind, and I have been thinking of how to make the keys themselves secure as well as how to build trust in the keys. 

I have two use-cases in mind. One where I want user actions on a central server to be signed, so if an adversary acquires access to the server, s/he still cannot impersonate the user. Therefore I assume that there is a central entity that can act as a trusted source, kinda like a CA.
The other is for content providers to sign their content, because some adversary might try and impersonate the author because s/he is trustworthy among their readers, but the method by which the content is delivered might not be very reliable (in the trust sense). This goes a bit in the way of "extraordinary claims require extraordinary evidence", "evidence" being the reputation/trust in the author.

Here's some concerns I've thought up:

* "Passphrase-space" is much, much smaller than "random bytes-space", but given a long enough passphrase it still is big enough that it can provide adequate entropy (brute-force attacks)
* ["your public key then effectively becomes a password hash, meaning anyone who sees it will be able to mount a dictionary attack"](http://crypto.stackexchange.com/questions/34727/can-i-always-derive-a-key-pair-from-passwordsalt-with-libsodium). In the CA use-case, the trust is the user being the only party having access to the secret key, so the public key wouldn't be shared with others than the CA. In the content author use case the public key would be shared with all readers and be generally available, and this is the use-case where a state sponsored adversary might want to try and crack the key.
* The passphrase would be stretched and hashed by a KDF to slow down generating dictionaries and brute-forcing. The username (or something like it) would be used as a salt to partition the key space for each user. However this would still mean that a per-user dictionary might predict future key pairs? I don't know if it would be sufficiently to make the KDF "expensive" to yield it impractical to generate a dictionary. [Source, though they say "short passphrase"](http://crypto.stackexchange.com/questions/1662/how-can-one-securely-generate-an-asymmetric-key-pair-from-a-short-passphrase?rq=1)
* Users will not be able to recover or revoke a key pair if they forget their passphrase. Though a CA might  be able to step in and sign old key pair as obsolete and a new key pair as trusted, however this requires the CA to have a root key pair. In the content author case the author would have to build their reputation from scratch.
* Changing passphrase means signalling the old key pair as obsolete and signing a new key pair with the old. Maybe draw inspiration from PGP revocation certificates. The CA can act as key server. This is safe (?) because an adversary would either need the private key from the CA or the most recent private key from the user to make a new key pair. If an adversary has either, all is lost. In the content author case only the author can signal the old key pair as obsolete.

Some pseudocode for the scheme:
```
kdf (input, salt, hardness) {}

function keypair(username, password) {
	seed = kdf(passphrase, username, constant)
	return keypair_from_seed(seed)
}
```

I hope my use cases are clear enough