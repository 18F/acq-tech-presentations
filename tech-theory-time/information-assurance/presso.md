class: left, top
# Information Assurance
the formal and more complicated name for computer security

### .right[what even is it?]

---

### Keeping secrets secret

Information assurance is about making sure people can only see the information
they're supposed to see, and ensuring that the information is what it claims
to be.

* Confidentiality
* Integrity
* Availability

???

This is the traditional information assurance triad.

---

### Keeping secrets secret

Information assurance is about making sure people can only see the information
they're supposed to see, and ensuring that the information is what it claims
to be.

* Confidentiality
* Integrity
* ~~Availability~~ .highlight[Authentication and Authorization]

Availability isn't ***strictly*** concerned with the security of information
but it is a critical part of .highlight[information assurance].  For our purposes,
availability can generally be considered .highlight[someone else's problem].

???

But for this talk, we're going to shift our focus a little bit.  Auth/auth
technically fall under confidentiality, but it's a complex topic and is more
relevant to us.

The "someone else" we leave to "availability" here is
operations staff, like the IT folks responsible for making sure the servers
stay up or that a denial-of-service attack is being dealt with.  It's a hard
job, but also not one that we will have to address very often.

---

### The balancing act

One of the first lessons of information assurance is that we must balance
security with the ability to do work (i.e., security vs. convenience).

--
count: false

## The "lock it all down" mentality is in direct opposition to one of the fundamental tenets of information assurance.

???

There's also a recognition that "perfect" security is impossible.  Instead,
we strive for "good enough," which takes into account the sensitivity of
the information and how hard someone is realistically likely to work to
get it.  The goal is to make it hard enough that an adversary won't bother,
or that if they do, it will take long enough that it's no longer relevant.

---

class: section, middle, center
# Confidentiality
making sure the neighbor reading your mail doesn't learn anything useful

---

### Confidentiality

1. Ensures that only the parties involved in a communication can see the
information in it
2. Ensures that outsiders cannot learn information based on the _shape_
of the data
3. Does ***not*** ensure that the information is what you think it is,
nor that you're talking to who you think you're talking to.

.highlight[Data] is a stream of stuff going past you. It doesn't necessarily
have any meaning. .highlight[Information] is the meaningful stuff you get
from data when you understand its context.

???
Data is just a bunch of zeroes and ones in a file. If you don't understand
the layout of the data, then it's meaningless to you. But if someone says,
"Hey, that's an Excel file," now it has meaning. You open it up and view
the information the data conveys.

---

### Confidentiality

# .white[Physical space]
.loud[Confidentiality in meatspace]

---

### Confidentiality / .white[Physical space]

In the physical world, confidentiality is easy to understand (though sometimes
hard to implement):

* Face-to-face conversation
* Handing a note directly to the person you want to read it
* Having meetings in a sound-proof room
* That SCIF-life

---

### Confidentiality

# .white[Cryptography]
.loud[Confidentiality in the digital world]

---

### Confidentiality / .white[Crypto]

Cryptography is the study of secure information transmission. It includes
encryption, decryption, secure hashing, secure random number generation,
and more.

It assumes that other people already have access to your communications
channel and attempts to make it impossible for them to read your
information even though they can see your data.

---

### Confidentiality / .white[Crypto]

Encryption is mixing up some information so people can't read it
without knowing how it was mixed up.

<table cellspacing="0" cellpadding="0">
  <tr class="first-row">
    <td>a</td>
    <td>b</td>
    <td>c</td>
    <td>d</td>
    <td>e</td>
    <td>f</td>
    <td>...</td>
  </tr>
  <tr class="second-row">
    <td class="empty"></td>
    <td class="empty"></td>
    <td>a</td>
    <td>b</td>
    <td>c</td>
    <td>d</td>
    <td>...</td>
  </tr>
</table>

.loud[c] becomes .highlight[a], .loud[d] becomes .highlight[b],
.loud[e] becomes .highlight[c], and so on...

---

### Confidentiality / .white[Crypto >] .highlight[Example]

Encryption has four parts: .highlight[plaintext], .highlight[cipher], .highlight[key],
and .highlight[ciphertext].

.center[![](encryption01.png)]

---

### Confidentiality / .white[Crypto >] .highlight[Example]

That earlier example is real encryption!

<table cellspacing="0" cellpadding="0">
  <tr class="first-row">
    <td>a</td>
    <td>b</td>
    <td>c</td>
    <td>d</td>
    <td>e</td>
    <td>f</td>
    <td>...</td>
  </tr>
  <tr class="second-row">
    <td class="empty"></td>
    <td class="empty"></td>
    <td>a</td>
    <td>b</td>
    <td>c</td>
    <td>d</td>
    <td>...</td>
  </tr>
</table>

This represents a cipher called .highlight[Caesar Shift] (or sometimes
.highlight[Caesar cipher]) with a key of .highlight[2]. The key is
the secret that tells you how the cipher was applied. In this case, it shifts the
letters by 2.

---

### Confidentiality / .white[Crypto >] .highlight[Example]

.center[![](encryption02.png)]

If you give someone the ciphertext and they know the key, they can decrypt
the plaintext.  Ideally, only people with the key can read the message.

???
This is really weak encryption.  The shape of the ciphertext gives us a lot
of information we can use to figure out the plaintext.  Look at the third word:
it's a single-letter word. How many of those are there?  Just two.  So C must
either be A or I.  Now if we can figure out one more letter, we will know the
key and we can decrypt the message.

---

### Confidentiality / .white[Crypto >] .highlight[It's hard!]

* Don't want to accidentally reveal anything
  * "shape" of the ciphertext (frequency of letters, number of words, length of
    information, etc.) can tell you about the plaintext
  * the cipher that was used makes it easier to attack the ciphertext
  (.highlight[life pro tip:] .loud[don't treat the cipher as a secret])
* Don't want to create weaknesses in the cipher
  * bad random number generation
  * mathematical oddities
  * "magic" numbers (i.e., back doors)

???

Only the key should be considered a secret.  In some cases, it's possible to
figure out what cipher was used based on the ciphertext and that is
considered completely okay.

### NSA magic number

NSA may have picked parameters for an algorithm that are highly correlated
mathematically, in a way that is difficult to prove.  If so, they created a
backdoor in that algorithm.

---
class: center, middle

.huge[SO DON'T EVER MAKE YOUR OWN]

---

### Confidentiality / .white[Crypto >] .highlight[It's hard!]

Always use well-known, well-established cryptographic ciphers, particularly those
vetted by NIST.  These ciphers have been carefully developed and researched
by dedicated cryptographers and mathematicians to root out as many hidden
mistakes as possible.

* Advanced Encryption Standard (AES)
* RSA
* Twofish

---

### Confidentiality / .white[Crypto >] .highlight[It's hard!]

Sometimes the well-known ciphers are later shown to have vulnerabilities. Here
are a few fairly common ciphers that are no longer considered safe and should
generally be avoided:

* Data Encryption Standard (DES)
* Triple DES
  * despite the name, it's only really about twice as strong as DES
* Rivest Cipher 4 (RC4)

On the internet, web servers that support these ciphers in SSL are considered
to be at risk.

???

### DES

The granddaddy of widespread ciphers, and the granddaddy of insecure ones.  Developed
in the 1970s, blessed by FIPS in 1977.  That blessing led to fast adoption,
but also lots of attention.  By the mid-80s, there were lots of theoretical ways to
break it, but in the late 90s, it was officially and practically broken.

### 3DES

The biggest problem with DES was the short, 56-bit key.  3DES was designed to allow
a longer key without redesigning the entire algorithm - they would have three 56-bit
keys instead of just one, or effectively 168 bits.  But there were some quirks that
resulted in only two of the keys being effective, so it was limited to 112 bits at
best.  But due to some other mistakes, NIST currently says it's effectively only 80 bits.

3DES is still considered secure enough by NIST, but the broader internet community
encourages moving away from it - it will probably be broken soon.

### RC4

It was created in 1987 and was super fast, leading to widespread adoption,
including in SSL (HTTPS).  But it was banned from SSL in 2015 - it was suspected
that state actors had the ability to break arbitrary RC4.

---

class: section, middle, center
# Integrity
making sure your neighbor didn't change your letters

---

### Integrity

In information assurance, integrity is *just* about making sure the information
you receive is the same information that was sent.  That is, nobody in the
middle changed anything.

---

### Integrity

# .white[Physical space]
.loud[Integrity in meatspace]

---

### Integrity / .white[Physical space]

In the physical world, integrity can be tricky:

* Check that the handwriting matches the sender's
  * like on those credit card signature slips that nobody ever looks at
* Check that your mail wasn't opened
  * like back in the old days when letters were sealed with wax seals
* Send them a text and ask if they really wrote that letter
* Send them an email asking if they got your text
  * don't do that

---

### Integrity
# .white[Cryptography]
.loud[Integrity in the digital world]

---

### Integrity / .white[Crypto]

Yep, cryptography again.  But this time, we don't rely on encryption. Instead,
we rely on one-way algorithms that transform some data into some other data
in such a way that it cannot be transformed back.

...That really sounds useless, doesn't it?

---

### Integrity / .white[Crypto]

These algorithms are called cryptographic hash functions. When you put some data
in, the result is called a hash (sometimes they're called digests or fingerprints).

`hash("Hello world") => 3e25960a79dbc69b674cd4ec67a72c62`

.highlight[(real example!)]

???

This is using a hash algorithm called MD5.

---

### Integrity / .white[Crypto >] .highlight[Hash properties]

1. **One-way**  
It should be impossible to go from a hash back to the original data

2. **Unique**  
Different data should *always* produce different hashes

3. **Repeatable**  
The same data should *always* produce the same hash

4. **Easy to make**  
Making a hash is mathematically easy

---

### Integrity / .white[Crypto >] .highlight[Use of a hash]

* Alice writes a letter to Bob and then computes the hash for the letter
* Alice puts the letter in the mail, and texts the hash to Bob
* When Bob gets the letter, he also computes the hash
* If Bob's hash matches the one he got from Alice, it's the same letter!
Otherwise, it has been tampered with.

This is called "fingerprinting" - using a hash to ensure the information you
received is the same information that was sent

???

out-of-band

This is a contrived example, you wouldn't actually do this by hand.
But if you have digital signatures turned on in your email, for example,
it does this for you behind the scenes.  It's a little more complicated
than our example, but this is the gist of it.

downloads

---

class: section, middle, center
# Authentication
who even *is* your neighbor?

---

### Authentication

Authentication is about verifying the truth or validity of something.
In computer world, we are most often talking about verifying a
person's identity.

---

### Authentication

# .white[Physical space]
.loud[Authentication in meatspace]

---

### Authentication / .white[Physical space]

1. **Driver's license**
> It has a photograph, name, and security features that we can check
to verify that the holder is who they say they are

2. **Iris scan**
> Iris patterns are believed to be completely unique. If your iris
matches the one on file, you must be that person

3. **Speakeasy**
> Walt sent me

---

### Authentication

# .white[Passwords and more!]
.loud[Authentication in the digital world]

---

### Authentication / .white[Shared secret]

If you know a secret and you tell me, then I can verify your identity
by asking you to tell me that secret again.

The canonical example is a .highlight[password].  Combined with your
.highlight[username], I can know who you are...

.loud[...as long as nobody else knows your password...]

---

### Authentication / .white[Two-factor]

Something you know, something you have, something you are. Pick two.

* **you know...** passwords
* **you have...** your cell phone
* **you are...** a fingerprint

???

know - financial services; addresses, car, loans, etc.

---

class: section, middle, center
# Authorization
preventing your neighbor from reading your mail in the first place

---

### Authorization

Authorization is about making sure people can only see and do the things
they're supposed to be able to see and do.  This requires being able to
.highlight[authenticate] people.

---

### Authorization

# .white[Physical space]
.loud[Authorization in meatspace]

---

### Authorization / .white[Physical space]

1. **Walls**
> Limits the options of people trying to enter a building to just openings
like doors and windows

2. **Guards**
> Security guards prevent people from entering a place unless they're authorized

3. **Lock & key**
> Locks keep people from accessing things unless they have the key

---

### Authorization

# .white[Access Controls]
.loud[Authorization in the digital world]

---

### Authorization / .white[Access control >] .highlight[Walls]

Like in physical space, we can have "digital walls" that prevent access to digital
resources.  Mostly these are .highlight[firewalls], devices that sit on the network
and deny access to internal assets from outside.

???

We can use a VPN to make a private connection to the internal network from outside.
That way, we can access stuff that the firewall is protecting.

---

### Authorization / .white[Access control >] .highlight[Guards]

We also have "guards" that only allow authorized access

* Access control lists say who can log into computers
* Permission required to access someone else's files on Google Drive
* Your phone only unlocks for ***your*** thumbprint, not all of them

These guards are all software that has to be carefully checked to verify that it
is checking the user's credentials and only allowing the access they're supposed
to have.

---

### Authorization / .white[Access control >] .highlight[Guards]

Guards can check for a lot of things

* Do you have access to this website?
* Do you have permission to edit blog posts?
* Do you have permission to merge a pull request?

These are called .highlight[permissions].

---

class: section
### Authentication and authorization

They are similar, and they generally go hand-in-hand.  Once we authenticate a person,
we then authorize them to see and do things.

* When you arrive at the airport, you show your driver's license to security.
They scan it with the little blacklight.  They are .highlight[authenticating]
your driver's license and validating that you are who claim to be.
* When you board the aircraft, you scan your boarding pass.  The boarding agent
is .highlight[authorizing] you to take a seat on that particular flight but
not any of the other ones.

---

class: middle center
# .white[Questions?]
