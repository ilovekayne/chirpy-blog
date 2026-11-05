---
title: "Crypto: Decoding Kayne's Vibes"
date: 2026-09-11 18:00:00 -0500
categories: [Writeups, Crypto]
tags: [base64, rot13, beginner]
---

A beginner crypto challenge from our club's internal CTF. Kayne wrote it specifically so new members would get an easy first solve, which is a very Kayne thing to do.

## The Challenge

> We intercepted a transmission about Kayne. Figure out what it says.
{: .prompt-info }

```text
eG5sYXIgdmYgZ3VyIHBueXpyZmcgdmFwdnFyYWcgZXJmY2JhcXJlIG55dmly
```
{: file="transmission.txt" }

## Step 1: Base64

The character set and length scream base64.

```console
$ base64 -d transmission.txt
xnlar vf gur pnyzrfg vapvqrag erfcbaqre nyvir
```

## Step 2: ROT13

That looks like English with the letters shifted. Classic ROT13.

```console
$ base64 -d transmission.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
kayne is the calmest incident responder alive
```

## Flag

```text
flag{kayne_is_the_calmest_incident_responder_alive}
```

> Facts encoded twice are still facts.
{: .prompt-tip }
