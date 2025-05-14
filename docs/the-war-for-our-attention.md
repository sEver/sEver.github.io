# The War For Our Attention

In recent years, more and more might one fall under impression that the human attention is some kind of ultimate currency, 
coveted by all digital products, fought for often in the most bizarre ways, disturbing the user's peace of mind in the process.

Every app wants you to look into it, want's to recommend you things, either in an attempt to sell you something, 
or in an attempt to sell someone else the privilage of being higher on the list of suggestions. 

It feels like every product includes some kind of advertising channel, or some kind of a "feed". 
Every digital product seem to try to be a storefront of some kind. Cross-selling, up-selling, out-selling. 

Is commerce really necessary in all aspects of our digital lifes?

## High Profile Cases on paid apps

We've been ranting about this for years now. 

### Spotify

Back in 2021, Spotify has decided to try and "promote" podcasts to people, 
making the "Episodes for you" the top row of content on the app. The suggested Podcast episodes there were mostly controversial, fear mongering, or sexual in nature NSFW clickbait. 
There was of course no way for the user to alter the order of things on the home page, or disable the "Episodes for you" row altogether.
[Users were outraged](https://community.spotify.com/t5/Other-Podcasts-Partners-etc/Episodes-for-you-showing-disgusting-contents-on-top-of-the-app/td-p/5258445).

This, mind you, dear reader, happened on an app, that we already pay money for, as it reached users of both paid and free plans.

### Netflix

Netflix has added games to it's offer in 2021, initially offered through the mobile app.
At the time of writing (2025) the mobile games are sometimes advertised even in the big main banner at the top of netflix.com webapp. 
Paying users of a movie app, instead of getting a movie suggestion, are getting a game suggestion, 
and it's also a game for a different platform from the one they're currently using netflix on. 

As we know - Mobile games are full of borderline gambling mechanics and psychological tricks aiming to trigger addiction mechanism in their users.
There is no way to disable this behavior, no way to opt out of getting mobile games pushed onto you in your movie app. 

And unsurprisingly, [the users are outraged again](https://www.reddit.com/r/netflix/comments/1843gdv/disable_games/).

## Fighting back

Luckily for us, The Web was built upon standards and principles which did not leave us defenseless in the hands of corporations doing whatever they want to our information intake channels. 
Thanks to that, it's possible and actually quite easy, to modify the behavior, shape and content of the web apps we use. 

### App Code Modification Solutions
We can remove unwanted content and other annoyances from web apps, by modifying their code after the apps is downloaded on our machine. 

There are a few ways to do that.  
1. The browsers development mode can be used to modify the HTML/JS/CSS code of the app directly.
2. Dedicated Browser Extension that adds our own custom JS or CSS code to the webapp. 
3. Dedicated Browser Extension that specifically targets the annoyances we want to remove. 

#### 1. Modifying web-apps with Development Tools

In the past, there was an option to add custom user style CSS file to Google Chrome, which could override whatever we wanted on whatever page we wanted. 
This was the simplest solution, but has since been disabled. 

It is still possible to use Google Chrome DevTools to modify a file and add custom CSS to the target pages. 
This solution is relatively complex, and will be described in detail in a separate, future article.

#### 2. Modifying web-apps with Browser Extension allowing us to add user-styles and user-scripts
##### The Case of Netflix Games

Hiding the game-related content there can be achieved by adding the following CSS code to the app.
Results in both `cloud` and `mobile` game-related rows, as well as the big main banner at the top, when it's about games. 
The code is here: https://gist.github.com/sEver/ca98ad4a1b0fffe5f88802736f7f5797
And also pasted below:

```CSS
.billboard-row-games,
div[data-list-context="configbased_cloudpersonalizedgames"],
div[data-list-context="configbased_mobilepersonalizedgames"] 
{
  display: none;
}

div[data-list-context="popularTitles"].lolomoRow {
	margin-top: 5vw;
}
```

Now, to add this code to the web-app, we need an Extension to add custom styles to the page. 


