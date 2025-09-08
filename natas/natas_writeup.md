# NATAS

## Natas0
**Username:** natas0
**Password:** natas0
**URL:** http://natas0.natas.labs.overthewire.org
**Flag/Next Password:** 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq

**Notes:**
Check the page source using `right-click` and `view page source`. The password is in a html comment.

## Natas0 → Natas1
**Username:** natas1
**Password:** 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
**URL:** http://natas1.natas.labs.overthewire.org
**Flag/Next Password:** TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI

**Notes:**
In this `right-click` is blocked. To check page source use shortcut `Ctrl-U`.

## Natas1 → Natas2
**Username:** natas2
**Password:** TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
**URL:** http://natas2.natas.labs.overthewire.org
**Flag/Next Password:** 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH

**Notes:**
In page source there is an image tag with file path `/files/pixel.png`. The image file is just a pixel. But visit path `/files` there are multiple
files `pixel.png` and `user.txt`. Flag for natas3 is in the `user.txt` file.

## Natas2 → Natas3
**Username:** natas3
**Password:** 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
**URL:** http://natas3.natas.labs.overthewire.org
**Flag/Next Password:** QryZXc2e0zahULdHrtHxzyYkj59kUxLQ

**Notes:**
In the page source there's a comment `No more information leaks!! Not even Google will find it this time...`. Paying attention to this comment
there's a hint `Google cannot find the file`. With little knowledge and research about this topic there's a way to prevent google to crawl through
files and paths using `robots.txt`. In this file there's a path `/s3cr3t`. At this path there's a file `user.txt` which contain password for next
level.

## Natas3 → Natas4
**Username:** natas4
**Password:** QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
**URL:** http://natas4.natas.labs.overthewire.org
**Flag/Next Password:** 0n35PkggAPm2zbEpOU802c0x0Msn1ToK

**Notes:**
The help message on page is that it's not allowed to access. The users should visit it from `http://natas5.natas.labs.overthewire.org/`. This
means request should be coming from `natas5` user rather than `natas4`. Using a request interceptor and changing the `refer` header to the
provided url will return flag/password for the next `natas5`.

## Natas4 → Natas5
**Username:** natas5
**Password:** 0n35PkggAPm2zbEpOU802c0x0Msn1ToK
**URL:** http://natas5.natas.labs.overthewire.org
**Flag/Next Password:** 0RoJwHdSKWFTYR5WuiAewauSuNaBXned

**Notes:**
After logging in the message shows that we are not logged in. Again after intercepting the request there's a value of `loggedin` which is `0` in programming
zero represents `false`. Changing this value from `0` to `1` and sending request will get our password.

## Natas5 → Natas6
**Username:** natas6
**Password:** 0RoJwHdSKWFTYR5WuiAewauSuNaBXned
**URL:** http://natas6.natas.labs.overthewire.org
**Flag/Next Password:** bmg8SvU1LizuWjx3y7xkNERkHxGre0GS

**Notes:**
In this challeng we need to provide some kind of secret. In page source we have logic how secret is getting checked. The secret is getting imported from
`includes/secret.inc` if we look into this file we can have our secret which can be passed in as input and get our password for `natas7`.

## Natas6 → Natas7
**Username:** natas7
**Password:** bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
**URL:** http://natas7.natas.labs.overthewire.org
**Flag/Next Password:** xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q

**Notes:**
In this challenge we have multiple pages on the machine. And in the page source have a hint that the password for web users path is
`/etc/natas_webpass/natas8`. The only difference is that page is getting accessed from the url variable. Which we can confirm by request after
removing variable value. We get an error which tell exactly what the page variable is doing. So we can get our password by using the path
provided in the comment.

## Natas7 → Natas8
**Username:** natas8
**Password:** xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
**URL:** http://natas8.natas.labs.overthewire.org
**Flag/Next Password:** ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t

**Notes:**
This challenge has a form which takes some sort of `secret` and a button to `view source code`.
In this source code we have logic how our input is getting compared and a `encodedSecret` and the function how our input is getting encoded. We
can simply reverse the encode function on `encodedSecret` which will give us our secret.

## Natas8 → Natas9
**Username:** natas9
**Password:** ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
**URL:** http://natas9.natas.labs.overthewire.org
**Flag/Next Password:** t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu

**Notes:**
In the source code the program is exceuting the terminal command without input filteration so we can do any command contactination or combine it
with simple this `cat /etc/natas_webpass/natas10` to complete this.


## Natas9 → Natas10
**Username:** natas10
**Password:** t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
**URL:** http://natas10.natas.labs.overthewire.org
**Flag/Next Password:** UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk

**Notes:**
This time the input is blocking certain characters like `/ ; &` so they cannot be used. So we use filtering bypassing techniques.
I am using `.* /etc/natas_webpass/natas11` to get the password.

## Natas10 → Natas11
**Username:** natas11
**Password:** UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
**URL:** http://natas11.natas.labs.overthewire.org
**Flag/Next Password:**

**Notes:**

## Natas11 → Natas12
**Username:** natas12
**Password:**
**URL:** http://natas12.natas.labs.overthewire.org
**Flag/Next Password:**

**Notes:**

## Natas12 → Natas13
**Username:** natas13
**Password:**
**URL:** http://natas13.natas.labs.overthewire.org
**Flag/Next Password:**

**Notes:**

## Natas13 → Natas14
**Username:** natas14
**Password:**
**URL:** http://natas14.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas14 → Natas15
**Username:** natas15
**Password:**
**URL:** http://natas15.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas15 → Natas16
**Username:** natas16
**Password:**
**URL:** http://natas16.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas16 → Natas17
**Username:** natas17
**Password:**
**URL:** http://natas17.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas17 → Natas18
**Username:** natas18
**Password:**
**URL:** http://natas18.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas18 → Natas19
**Username:** natas19
**Password:**
**URL:** http://natas19.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas19 → Natas20
**Username:** natas20
**Password:**
**URL:** http://natas20.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas20 → Natas21
**Username:** natas21
**Password:**
**URL:** http://natas21.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas21 → Natas22
**Username:** natas22
**Password:**
**URL:** http://natas22.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas22 → Natas23
**Username:** natas23
**Password:**
**URL:** http://natas23.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas23 → Natas24
**Username:** natas24
**Password:**
**URL:** http://natas24.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas24 → Natas25
**Username:** natas25
**Password:**
**URL:** http://natas25.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas25 → Natas26
**Username:** natas26
**Password:**
**URL:** http://natas26.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas26 → Natas27
**Username:** natas27
**Password:**
**URL:** http://natas27.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas27 → Natas28
**Username:** natas28
**Password:**
**URL:** http://natas28.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas28 → Natas29
**Username:** natas29
**Password:**
**URL:** http://natas29.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas29 → Natas30
**Username:** natas30
**Password:**
**URL:** http://natas30.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas30 → Natas31
**Username:** natas31
**Password:**
**URL:** http://natas31.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas31 → Natas32
**Username:** natas32
**Password:**
**URL:** http://natas32.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas32 → Natas33
**Username:** natas33
**Password:**
**URL:** http://natas33.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

## Natas33 → Natas34
**Username:** natas34
**Password:**
**URL:** http://natas34.natas.labs.overthewire.org
**Flag/Next Password:**
**Notes:**

---

## Progress Summary
- **Completed Levels:** 10/35
- **Current Level:** natas11

## General Notes
- Remember to check page source, network requests, and cookies
- Use browser developer tools extensively
- Document interesting techniques and vulnerabilities encountered
