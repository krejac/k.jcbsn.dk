---
layout: post
title: Python - Send mail
---

**[TL;DR](http://en.wikipedia.org/wiki/Wikipedia:Too_long;_didn't_read)** - Det er lige gået op for mig, *hvor* nemt det egentligt er at sende en gmail med Python. Det må jeg lige få noteret...

![Code...]({{ site.url }}/public/assets/20141023_code.jpg "Code...")

Nedenstående eksempel sender en email til 'user2@example.org' med en påmindelse om at medbringe en paraply (det kunne jo være en del af et script, der tjekkede sandsynligheden for regn. Ja, det skal jeg også have lavet...).

	:::python
	import smtplib

	# Credentials
	GMAIL_USERNAME = 'user1@example.org'
	GMAIL_PASSWORD = 'xyz123!'

	# Contents (body_of_email can be either plaintext or html)
	email_subject = 'Email subject goes here'
	recipient = 'user2@example.org'
	body_of_email = """Dear XXX,<br>
	Don't forget to bring an umbrella. It's going to be raining cats and dogs...<br>
	<br>
	See you soon.<br>
	<br>
	Sincerly,<br>
	UNIVAC
	"""

	# Establish secure connection, verify identity (you may have to create an app specific password if you - like me - have two factor authentification enabled).
	session = smtplib.SMTP('smtp.gmail.com', 587)
	session.starttls()
	session.login(GMAIL_USERNAME, GMAIL_PASSWORD)

	headers = "\r\n".join(["from: " + GMAIL_USERNAME,
                	       "subject: " + email_subject,
            	           "to: " + recipient,
        	               "mime-version: 1.0",
    	                   "content-type: text/html"])

	content = headers + "\r\n\r\n" + body_of_email
	session.sendmail(GMAIL_USERNAME, recipient, content)

Og da smtplib er implementeret i [Pythonista](http://omz-software.com/pythonista/), burde ovenstående eksempel virke der også. :)
