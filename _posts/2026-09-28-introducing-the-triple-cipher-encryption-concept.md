---
layout: post
title: "Introducing the Triple Cipher encryption concept"
date: "2026-09-28 10:50:40 +0200"
categories: ["Security", "Encryption"]
author: Iain Cambridge
---
I was talking to some folk at [GCHQ](https://www.gchq.gov.uk) about an idea they got told about. I told one person that I wanted to make three unique encryption ciphers for a project, and they got told I wanted to make a “triple cipher” cipher. They said that it sounded good, but it’s just encrypting something three times and is rather basic. After I pointed out what my original idea was, I started brainstorming, and this is the idea I came up with to make a Triple Cipher without just encrypting it three times one after another but using those three different keys to interweave to create a dual layer encrypted file.

## Concept

Instead of encrypting a file in one go, the file is chunked up bittorrent style and then encrypted using two different ciphers and then the results from that are concatantated into a single file and that file is encrypted again.

That results in an attacker breaking the first layer of encryption and getting another layer and thinking that it’s just another straight layer and try to encrypt that. Which would be impossible because it’s two different ciphers mixed up.

## Mixing The Ciphers Up

The first thing you think of when you hear mixing the ciphers up is that you know to break it down into chunks and then break each one, knowing that one after another each part is using the other cipher. So chunk 1 using cipher 1, then chunk 2 is using cipher 2, and then chunk 3 is back to cipher 1. While it still makes it a pain in the ass to decrypt since you need to realise that it’s triple cipher in the first place, it’s some what predictable and therefore not that good.

Therefore, I suggested a pattern such as 1-3-2-1 or 2-5-1-3 where each number is the number of chunks for that cipher. So with 1-3-2-1 pattern, the first cipher is used once, then the next cipher is used for 3 chunks, then back to the first cipher for 2 chunks and then finally back to the second cipher for 1 chunk and repeat that pattern until the file is complete. If the file end before the pattern, it doesn’t matter because it’ll still be using the cipher for those chunks.

## Chunk Sizes

Another way to make it harder for an attacker to decrypt is to change the size of the chunks. My suggestion is to have the chunk size change each time. This means not only do they need to know that it’s Triple Cipher and the pattern but they also need to know the chunk sizes.

## Passphrase Metadata 

The issue now becomes: how does the decrypter know how to decrypt it since it needs to know the pattern and the chunk sizes. The original idea was to have metadata in the second layer of encryption. This was rejected in 5 seconds because it would give away that it’s a triple cipher file.

Instead, my idea is to create an algorithm that has a one way hashing (or something) that generates two things. We need to create the pattern and the chunk size. If we’re able to create them securely via a one way hashing method from the passphrase, then we’re able to avoid metadata telling us the pattern and chunking, so all the attacker will get is another layer of encryption.

Your passphrase is used with all three encryption keys. Or you can have it chunk up the passphrase into three different passphrases for your encryption keys.

## GCHQ Note

GCHQ say they don’t mind me telling people about this because they don’t have the capacity to create it so would love for someone to create an open source version to use.. And I don’t work for them, so I’m free to share my knowledge. And the name came from them since the idea came from me trying to come up with a way to have 3 ciphers in an encryption method.