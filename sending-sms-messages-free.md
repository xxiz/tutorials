# Sending SMS Messages For Free (via MMS)
This tutorial explains how you can send SMS messages for free via MMS. It works by using your carriers MMS/SMS gateway and sending a message to your phone number (if you have it enabled).

## Overview
### What is a MMS Gateway?
A MMS gateway is a service that allows you to send a message to a phone number via email. The message is then sent to your phone as an MMS message.

### Find your carrier's MMS/SMS gateway
You can find your carrier's MMS/SMS gateway by going to [freecarrierlookup.com](https://freecarrierlookup.com/), or looking your ISP's default gateway address.

### Sending a message
To send a message, you need to send an email to your carrier's MMS/SMS gateway. The email should have the following format:

    To: <your phone number>@<your carrier's MMS/SMS gateway>
    Subject: <your message>
    Body: <your message>

## Example
### Sending a message
To send a message to `+1 (555) 532 5355` who is a Rogers customer, with the message `Hello World!`, you would send an email to `5555325355@pcs.rogers.com` with the body set to `Hello World!`.