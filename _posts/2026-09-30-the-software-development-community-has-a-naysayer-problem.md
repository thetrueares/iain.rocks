---
layout: post
title: "The software development community has a naysayer problem"
date: "2026-09-30 08:50:40 +0200"
categories: ["Security", "Encryption", "Opinion"]
author: Iain Cambridge
---
I recently wrote a blog post outlining a new encryption concept ["Introducing the Triple Cipher encryption concept"](/blog/introducing-the-triple-cipher-encryption-concept). This is literally a concept and not a whitepaper on this idea. This idea came from a conversation with a few folk at [GCHQ](https://www.gchq.gov.uk) where we talked about it because someone had mistakenly told them I wanted to build one when I was saying it would be cool to properly study encryption and build three unique ones for myself. Once I pointed out the truth, I then started to think about how I could use three cyphers and not just do [cascading/multiple encryption](https://en.wikipedia.org/wiki/Multiple_encryption), after some brainstorming I came up with that concept, which got named “Triple Cipher” by the GCHQ team so they could mess with their encryption guys, who said it sounded good but stupid. Next thing you know all the audio is being wiped so it doesn’t leak it, so to protect that idea they were willing to wipe out 5 hours of audio logs of talking to me when the point of recording it was to get ideas from me. So I take that as a massive sign that the idea has serious potential. And the response from [r/programming](https://www.reddit.com/r/programming) was so bad it’s shocking, just non-stop naysayers with good-sounding comments that were generally flawed.

## Multiple Encryption

Many people seem to think that this would mean merging all the keys together instead of three different keys. They seem to think that you must merge all the keys into one key. One person insisted that encrypting something with two layers of 64-bit keys is the same level of secure as encrypted on one layer with a 128-bit key. Which sounds good, but the entire point of the layered encryption is that you make it a lot harder to know when you’ve cracked the first layer.

So while the theory of it being the same level of encryption just added together sounds good, it doesn’t really compute. You have two different ciphers you need to break, and you need to know when you broke the first cipher and if all you get back is data that looks like garbage you got from other failed attempts. So the fact that you have an extremely hard time knowing you broke the first cipher makes it way more secure. And the fact you need to work on two different ciphers makes it more secure by default. Because you need to do the foundational work of cracking it twice instead of just once.

This response is basically saying the [NSA](htttps://www.nsa.gov) is wrong. They are the leading experts in the world for encryption but they’re wrong on encryption? NO! Check your egos!

## Security via Obsfucation

*“Security via obfuscation in encryption? We’re done here.”*

I got this response many times. Many people seem to fail to understand that encryption is literally obsfucating the data. You’re changing the data so people can’t understand it, and it can be un-obfuscated, aka decrypted which is the entire point. Some compared it to changing variable names in JS code when minifying it.

*“Hiding what you’re doing in encryption doesn’t make it any more secure.”*

This comment makes no sense since encryption is obfuscation, and obfuscation is hiding what you’re doing. So if encryption is hiding what you’re doing, then hiding it even more makes a lot of sense. And if obfuscation is security, then adding more clearly makes it more secure.

## Security via Obsecurity

The number of people who called this concept security via obscurity is shocking. It’s a new concept, but just because it’s a new idea doesn’t mean the point of it is to be obscure.

I was accused multiple times of not knowing what security via obscurity actually means one time after I literally gave an example of using an obsecure HTTPd over Nginx because it’s less likely an attacker can exploit it because fewer people are looking at that HTTPd to find vulnerabilities.

You also have the idea of changing the HTTP headers to pretend to be a different HTTPd which people think is security via obscurity. But that’s just obfuscation, really. You’re obfuscating what you’re running while running a common HTTPd.

Many things doing this is just a pointless thing and makes things less secure. Yet, the top security experts in the world know it’s an extra layer. Google do it. That’s one of the reasons they have a custom HTTPd; it’s a lot harder to exploit an HTTPd if your only access to it is via HTTP on servers you don’t have access to without access to the code.

And if we go down the verb route of obscuring something to make it difficult to see, hear, read, or understand. Then that is exactly what encryption is. Making it diffcult to read.

## It’s a process not an algorithm.

Like plain cascading/multiple encryption, it’s not an algorithm in itself it’s a process of doing it. However, folk focused on saying things such as merging three keys into one means it’s a single cipher. But at no point did I mention merging three keys, nor did I even think about merging the keys.

This concept, as is, is just an encrypter and decrypter application that uses other ciphers together to create a pain in the ass to crack.

## Kerckhoff’s Principle

People then suggested this violates Kerckhoff’s principle because you’re adding multiple things they need to know to crack it. Just because you added more things you need to crack to make it harder to crack. Doesn’t mean that it’s any less secure because you know those things. It just means you know how much more work you have to crack.

The data is encrypted using secure algorithms, third-party, and just encrypted in parts, which has nothing to do with how secure the cryptography is. The fact that you need to decrypt parts using different algorithms doesn’t make it any less secure.

The plan is for this to become an open and well-known way of doing it like 3DES. So there is no point where this is only secure because they don’t know the method exists. It’s just more secure if no one knows it is exists, and that is only by 0.0001% or some silly low percentage like that. You can know everything, and it’s still a massive pain in the ass to decrypt, but if you don’t and you just have the file and the keys, it’s an even bigger pain in the ass to decrypt.

## Conclusion

This is probably the best example of how bad the software community actually is. It was a bunch of naysayers who GCHQ called “Script Kiddie cybersecurity experts” because they were just parroting things they’ve heard about security without truly understanding them.

Literally, just a bunch of naysayers, many of whom, when I responded to clearly, didn’t understand the concept and, in some cases, didn’t read the blog post because they didn’t know about the GCHQ note, which is a paragraph at the bottom, so if you didn’t see that, you didn’t read it.

One guy in my opinion, pretended to be someone from GCHQ, and when I asked them to open up their DMs so I could identify myself properly using a verifier codename, they didn’t. And then insisted I was name-dropping when I said they can ask around GCHQ to see what others thought since they want it, they just lack capacity. This was a Reddit moderator who ended up getting me banned once I gave my verifier, and he actually realised he was wrong. That’s how petty and sad the Reddit moderators are; they pretend to be someone else to win points and get you banned when they lose.
