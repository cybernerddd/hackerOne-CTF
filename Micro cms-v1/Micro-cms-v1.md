# CTF - Hackerone
- First flag was from a xss

- I first visit the ‘create a new page’ link. When I create a new page, the details of the new page are reflected in the response.
- Good indication the website is vbulnerable to xss
- Drop it with my G0-to payload:

`hello<script>alert(1);</script>`
First flag was revealed/

## Second Flag was SQLi
- When editing a page, I notice that the page id is passed in the URL
- I placed a ‘ (single quote) at the end of the id parameter and I get the second flag
- Looking like this:
`https://be8f9d90c1f866fa7e4f5111edd5f18b.ctf.hacker101.com/page/edit/1'`

## Third Flag was Unauthorized Access
- I saw that whenever I open a page, the ID was visible in the URL
- I tried starring from 2 and on the 4th page landed mt flag
`https://be8f9d90c1f866fa7e4f5111edd5f18b.ctf.hacker101.com/page/edit/4`

## Last Flag was Digging in XSS(with markdown the clue)
- Found out `Markdown` is supported, but scripts are not in editing the ID 1
- Used an **HTML Injection using <img> with onerror-based XSS**
  this:
  `<img src=x onerror=alert('XSS')>`

   ## code explained below
  
`<img src=x>`: The browser tries to load an image from a broken source (x is invalid)
`onerror=alert('XSS')`: When the image fails to load, the onerror event fires — triggering the alert('XSS').
