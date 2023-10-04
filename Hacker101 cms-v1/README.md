# HACKER101 CTF CMS-V1 Write-up

## 1st flag
I created a page and passed arbitrary input. Checking the `inspect page` of the website revealed the flag in the form of a script.

Clicking on `go home` button also generates an alert that reveals the same flag.


## 2nd flag
Looking at the url we can see that the page ID is passed on in the url meaning this website maybe vulnerable to sql injection.

Placing a `'`(single quote) at the end of the url didn't work but adding a `'` while editing the page reveals the second flag.
 
## 3rd flag
Looking at the url, we can see that page ID is passed on in the url itself. This is a case of broken access control.

Upon inspecting the web page, I found that the pages that were already there had an ID of `1` and `2` but the pages that I made had their ID's starting from `8`.

So I started passing ID's from `3` to `7`. All other ID's except gave me a `404` error except ID number `5`.

ID `5` gave me a `403 forbidden error`. I tried adding `/edit/5` and this gave me the flag.

## 4th flag
On the create new page, it is specified that `markdown` is supported but scripts are not, so we have to find a way to bypass markdown filter to execute XSS.

Adding this text in text box -> `<button onclick=alert("Text")>Button</button>` adds a button on the page. On clicking the button, nothing special happens but on inspecting the page, we can see that the last flag is displayed as an attribute of the `button` tag.
