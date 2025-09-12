---
author: "Rajshree"
title: "ImaginaryCTF 2025 Web Challenges Writeups"
date: "2025-09-11"
---

### Certificate
This was probably one of the simpler challenges in the web category for this  CTF. The goal was to extract the flag for the name `Eth007` but the caveat was - every time you typed in that particular name. It would appear as `REDACTED` instead.
tty
The first thing I was to Inspect --> Sources and there I found that it was using a function to calculate the flag for each name. And if name was `Eth007` it would replace it with `REDACTED`.

![cert-chall](/imaginary-ctf-2025/cert-chall.png)

The solution to this challenge was simply calculating the `customHash` for the name `Eth007` which came out to be `d5e06bd5` so the flag was `ictf{d5e06bd5}`


### Imaginary Notes

This was a very fun challenge to solve and easy one as well. At first it did look a little deceiving at first but once I started looking around it did become more clear.

The flag was stored as a password in a supabase for admin. I did insptect --> sources and under app there was a js file where they left the link to the database along with the apikey. Once I saw that, the challenge was theoretically solved.

![s1](/imaginary-ctf-2025/s1.png)

When I tried to access the link, it gave me an error that no `apikey` was attached in the header request. So I decided to use BurpSuite to capture the request and modify it. I just had to add the `apikey` and `Authorization: Bearer` in the request.

![s2](/imaginary-ctf-2025/s2.png)


![s3](/imaginary-ctf-2025/s3.png)


After forwarding the request, I had access to the database and I could very easily see the flag/password.

![s4](/imaginary-ctf-2025/s4.png)


