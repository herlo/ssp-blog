---
title: Thinking About File Encryption (again)
author: herlo
layout: post
date: 2007-03-08T16:22:58+00:00
url: /2007/03/08/thinking-about-file-encryption-again/
categories:
  - Editors
  - Tech
  - Tools

---
Some of you might recall my article the other day about **vim** encryption. It is a very nice way to encrypt the file but has some holes in the process. Having extra files laying around while the encrypted file is open is not good enough, though with enough physical security it could be fairly safe.

Along comes **gpg** with another option for me to try. I've spent a fair amount of time digitally signing my documents with my gpg key. I've distributed my public key and kept my private key safe as well for when I do need to decrypt something important.

Today in my travels around the interweb, I came across a bit about gpg encryption and thought that it might be able to accommodate my request of a simple encryption utility for my _passwords_ file. So lets have a look at it and see the results.

The simplest thing to do is to take my unencrypted _passwords_ file and encrypt it with gpg:

`$ gpg -c passwords`
  
`Enter passphrase:  <strong>my pass phrase</strong>`
  
`Repeat passphrase:  <strong>my pass phrase</strong>`
  
`$ ls passwords*`
  
`passwords  passwords.gpg`

Well, there's my problem, right there. Did you see it? I did! The problem is that I now have two files, one encrypted and one not. I don't want the unencrypted one anymore now that I have the encrypted one. Except, what if the encrypted one didn't work? What if I lose the encrypted file, what if it's on a bad block? Well, there's my dilemma. And I am still waiting for a better solution, ho hum, I guess I'll keep looking.

Meanwhile, back at the **gpg** ranch, I'll show you how to decrypt the file so you can read it again.

`$ gpg passwords.gpg`
  
`gpg: CAST5 encrypted data`
  
`Enter passphrase:  <strong>my pass phrase</strong>`
  
`gpg: encrypted with 1 passphrase`

And my file is restored to its original state. This is good for sure, but I think it isn't quite what I am looking for&#8230; Thank you for trying **gpg**, I'll keep looking. **vim** encryption seems appropriate for now.

Cheers,

Herlo