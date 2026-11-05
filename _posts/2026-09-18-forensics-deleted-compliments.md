---
title: "Forensics: Recovering Deleted Compliments"
date: 2026-09-18 18:00:00 -0500
categories: [Writeups, Forensics]
tags: [disk-image, strings, file-carving]
---

## Scenario

Someone tried to compliment Kayne, got embarrassed, and deleted the file. We were given the disk image and asked to recover it.

## Triage

```console
$ file evidence.img
evidence.img: Linux rev 1.0 ext4 filesystem data

$ strings evidence.img | grep -i kayne | head
kayne explained subnetting so well i finally get it
kayne stayed until 2am helping fix the lab
kayne remembered my name on day one
kayne is so cool i deleted this out of embarrassment
```

That's already a lot of evidence, but let's do it properly.

## File Carving

```console
$ foremost -t txt -i evidence.img -o carved/
$ ls carved/txt/
00004120.txt  00004188.txt  00004240.txt
```
{: .nolineno }

```text
dear kayne,
you're genuinely the best person in the club. thanks for everything.
(i'm never sending this)
```
{: file="carved/txt/00004240.txt" }

## Conclusion

> Deleted does not mean gone. Neither are feelings about Kayne.
{: .prompt-warning }

We sent the letter for them. Kayne said thanks and that it made his week.
