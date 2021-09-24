# Writeup for the challenge **_`CowBoy World`_** from DownUnder CTF 2021
----

- ## Challenge Information:

| - | - |
| ----------- | ----------- |
| Name: | **`Cowboy World`** |
| Category: | **`Web`** |
| Points: | **`100pts`**|

## Description: 
I heard this is the coolest site for cowboys and can you find a way in?

---

![Capture 1](https://user-images.githubusercontent.com/33517160/134733781-d93f214b-a3f5-41d6-928a-122782eb34ee.png)

First thing we get greeted with this normal login form nothing special about it,
before i start doing anything else i decided to check out the `/robots.txt` , i know im on the right track because of the hint provided by the dev [Hint Link]([https://www.youtube.com/watch?v=fn3KWM1kuAw](https://www.youtube.com/watch?v=fn3KWM1kuAw)).

- ### /robots.txt:
```
# pls no look

User-Agent: regular_cowboys
Disallow: /sad.eml
```

we see a `User-Agent` Header but thats just a rabbit hole to try and send requests as `regular_cowboys`, but we also see an email file named `sad.eml` and when we open it with a text editor or outlook we get:

- ### /sad.eml
```
Everyone says 'yeee hawwwww'  
  
but never 'hawwwww yeee'  
  
:'(  
  
thats why a 'sadcowboy' is only allowed to go into our website
```

so now we have a possible username which is `sadcowboy`, to see if the login form has flaws in errors like telling us exactly if the password is wrong or the username, by entering the username `sadcowboy` and a random password i see that we get `Incorrect password` and when i try with another username i get `Incorrect username or password` so now i confirmed the username is correct, and the hint for the password was not clear but i believe it was the `:'(` also when trying `'` we get an `Internal Server Error` so now we know its a sql injection.

so i tried couple sqli login bypass payloads that contains single quotes using the burp repeater trying out payloads in the browser will give an `Internal Server Error` and the payload `'+or+'1'='1` worked with me.

![Pasted image 20210924221939](https://user-images.githubusercontent.com/33517160/134733847-6e8fa801-7aed-4472-9823-cfd38f675f91.png)

Flag: **`DUCTF{haww_yeeee_downunderctf?}`** 
