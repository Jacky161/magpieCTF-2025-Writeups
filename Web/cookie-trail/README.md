# cookie-trail - Category: Web

>New email from cors@nypd.gov:
>
>Jake Kaylined has had many aliases over the years, and Krypto has dealt with many of his online persona throughout her career. One such persona was "Spider". We believe that her involvement with this alias of Jake's might have relations to the case.
>
>Investigate the casefile regarding Spider and Krypto.
>
>Edward Cors - NYPD

![The Website](img/website.png)

We're greeted by a rather blank looking page. It seems everything in this challenge really wants us to look at our cookies. So let's do just that!

![Firefox developer tools, showing no cookies](img/cookies_initial.png)

Nothing?? Well, I suppose it would be too easy if there was something there. Taking a look through the HTML source doesn't reveal anything particularily interesting. Let's try just inputting something random and hitting search on the site.

![The Website after hitting search](img/website2.png)

Maybe now we'll have something in our cookies? And indeed we do!

![New cookie dropped](img/cookies_2.png)

My immediate thought is to try and mess around with this cookie. Let's just try changing the value to 1 and see what happens. If we do that and reload the page, we get a new part of the story!

![Part 1 of Spider's Story](img/website3.png)

If we keep increasing the number and refreshing, the story continues. After inputting a value of 10, we get the following:

![Part 10 of Spider's Story + the flag](img/website4.png)

Nice!

**Flag:** magpieCTF{chr15t1n@_3xp0$3d_$p1d3r}
