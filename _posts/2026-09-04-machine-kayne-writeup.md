---
title: "Machine Writeup: Kayne (Insane)"
date: 2026-09-04 18:00:00 -0500
categories: [Writeups, Machines]
tags: [linux, privesc, enumeration, insane]
---

> **Difficulty:** Insane. Not because he's hard to get along with, but because he's hard to keep up with.
{: .prompt-info }

## Enumeration

Started with the usual scan.

```console
$ nmap -sC -sV -p- kayne.cyberstout
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      KayneSSH (accepts any question, no auth needed)
80/tcp   open  http     nginx (serving: "how can i help?")
8443/tcp open  https    Incident Response Console
```

Port 80 just returns a page that says `how can i help?`. That's it. No vulnerabilities. Just an offer.

## Foothold

We tried every exploit we had. Nothing worked.

Eventually we read the page again and typed a question into the form. Kayne answered it, explained it, and then asked if we wanted to try the next part ourselves.

```console
$ cat user.txt
you got this by asking for help. that's the intended path.
```

> The intended foothold is literally just asking. Most people overthink it.
{: .prompt-tip }

## Privilege Escalation

Checked `sudo -l`:

```console
$ sudo -l
User you may run the following commands on kayne:
    (ALL) NOPASSWD: /usr/bin/learn
```

So we ran it. A lot. Every time Kayne taught us something, our privileges went up a little.

```console
$ /usr/bin/learn --from kayne --topic everything
[+] incident response .......... learned
[+] log analysis ............... learned
[+] staying calm ............... still learning
# whoami
root
# cat /root/root.txt
ZmxhZ3t3M19sMHYzX2s0eW4zfQ==
```

Decode that one yourself. (Hint: `base64 -d`.)

## Lessons Learned

- The box is not hard. The box is *kind*.
- Asking for help is a valid technique.
- We love Kayne.
