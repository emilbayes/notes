# Secret Sharing

## n = k = 2
When $n = k = 2$ a one-time pad can be used as it is very efficient and has the
same space requirements as Shamir's Secret Sharing Scheme. It yields the same
Perfect Secrecy guarentees as long as the key is for the one-time pad is chosen
at random. Otherwise the key might not have sufficient entropy, as the data
likely will have low entropy. Consider encrypting a JSON blob. The first couple
of bytes are almost guarenteed to be `{"` and so if the key contains any pattern
the first two bytes can be learnt here too and the search space is then much
smaller.
On the other hand, a random key, given that one-time pad
`cipher = key XOR plain`, will allow and attacker to construct any message from
the cipher. Hence no information can be learnt from either `key` or `cipher`,
even if the plaintext is known to have a certain structure. Another remark is
that `key` and `cipher` are interchangable, and can therefore be used as a part
of the secret.

## Further questions
* Can ECC be used to one-time pad with multiple, shorter keys?
* How can Fair Exchange be used by multiple parties to exchanges shares?
* How can cheaters be caught using Fair Exchange?
