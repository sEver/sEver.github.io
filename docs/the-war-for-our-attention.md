# The War For Our Attention

In recent years, more and more might one fall under the impression that the human attention is some kind of ultimate currency, 
coveted by all digital products, fought for, often in the most bizarre ways, disturbing the user's peace of mind in the process.

Every app wants you to look into it, want's to recommend you things, either in an attempt to sell you something, 
or in an attempt to sell someone else the privilage of being higher on the list of suggestions that are fed to you. 

It feels like every product includes some kind of advertising channel, or some kind of a "feed". 
Every digital product seem to try to be a storefront of some kind. Cross-selling, up-selling, out-selling. 

_Is commerce really necessary in all aspects of our digital lives?_

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
Mobile games are widely known to have the most toxic, player-abusing mechanics in gaming, and in general are not liked that much for it. 
Yet still. Netflix chose to push them on us. 
There is no way to disable this behavior in netflix, no way to opt out of getting mobile games pushed onto you in your movie app. 

And unsurprisingly, [the users are outraged again](https://www.reddit.com/r/netflix/comments/1843gdv/disable_games/).

## Fighting back

Luckily for us, The Web was built upon standards and principles which did not leave us defenseless in the hands of corporations doing whatever they want to our information intake channels. 
Thanks to that, it is possible, and actually quite easy, to modify the behavior, shape, and content of the web apps we use. 

We can remove unwanted content and other annoyances from web apps, by modifying their code after the app code is loaded on our machine. 

There are a few ways to do that.  
1. The browsers development mode can be used to modify the HTML/JS/CSS code of the app directly. (complex)
2. Dedicated Browser Extension that adds our own custom JS or CSS code to the webapp. (medium complexity, but quite versatile)
3. Dedicated Browser Extension that specifically targets the annoyances we want to remove. (easy)

### 1. Modifying web-apps with Development Tools

In the past, there was an option to add custom user style CSS file to Google Chrome, which could override whatever we wanted on whatever page we wanted. 
This was the simplest solution, but has since been disabled. 

It is still possible to use Google Chrome DevTools to modify a file and add custom CSS to the target pages. 
This solution is relatively complex, and will be described in detail in a separate, future article.

### 2. Modifying web-apps with Browser Extension allowing us to add user-styles and user-scripts
#### The Case of Netflix Games

Hiding the game-related content on netflix can be achieved by adding the following CSS code to the app.
Results in both `cloud` and `mobile` game-related horizontal rows, as well as the big main banner at the top, when it's about games, are hidden by it. 

[The code is available here](https://gist.github.com/sEver/ca98ad4a1b0fffe5f88802736f7f5797)
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

Now, to add this code to the web-app, we need a Browser Extension to add custom styles to the page, also known as `user-style`s.

#### What are User Styles? 

When CSS was being conceived, it was immediately obvious, that the author of a webpage can style it in a way that would not meet the needs or preferences of the user.

For this reason, the concept of a `User Style Sheet` was included in the design. 
A Style Sheet that can be defined by the User, to apply their own preferences to the web pages they were viewing. 

See some reference sources below:

> CSS, or Cascading Style Sheets, offers a flexible way to style web content, with styles originating from browser defaults, **user preferences**, or web designers. [...] this separation maintains the **accessibility and readability of the content**, ensuring that the site is **usable for all users**, including those **with disabilities**. Its multi-faceted approach, including considerations for selector specificity, rule order, and media types, ensures that websites are visually coherent and **adaptive across different devices and user needs**, striking a balance between design intent and **user accessibility**. -- https://en.wikipedia.org/wiki/CSS#Sources // emphasis the author

> One of the goals of CSS is to **allow users greater control over presentation**. Someone who finds red italic headings difficult to read **may apply a different style sheet**. Depending on the browser and the website, **a user may choose from various style sheets provided by the designers, or may remove all added styles, and view the site using the browser's default styling, or may override just the red italic heading style without altering other attributes**. -- https://en.wikipedia.org/wiki/CSS#Sources // emphasis the author 

> If a page's layout information is stored externally, a **user can decide to disable the layout information entirely**, leaving the site's bare content still in a readable form. Site authors may also offer multiple style sheets, which can be used to completely change the appearance of the site without altering any of its content. Most modern web browsers also **allow the user to define their own style sheet**, which can include rules that **override the author's layout rules**. This allows users, for example, to bold every hyperlink on every page they visit. -- https://en.wikipedia.org/wiki/Style_sheet_(web_development)#Customization // emphasis by the author

> In order to **ensure that users can control styles**, CSS2 changes the semantics of the "!important" operator defined in CSS1. In CSS1, authors always had final say over styles. In CSS2, if a **user's style sheet** contains "!important", it **takes precedence** over any applicable rule in an author's style sheet. This is an important feature to users who require or must avoid certain color combinations or contrasts, users who require large fonts, etc. -- https://www.w3.org/1999/06/NOTE-CSS-access-19990616 // emphasis by the author


#### Google Chrome Browser Extensions for user styles

This part needs a little history, as it seems people who embrace the core idea of the Web - that the user should have easy access to changing how the Web looks for them, are facing various difficulties on this path. 

##### Stylish and UserStyles.org - The first major `User Style Sheet` project, which after being sold, started stealing user data

While searching the web for "User Styles" You will most likely find: 
- `UserStyles.org` - a platform for publishing and sharing user styles.
- Browser Extension `Stylish` that has been downloaded by over 2'000'000 users. 

This was the User Style heaven for everyone, up until around 2016. The project was developed on GitHub (https://github.com/stylish-userstyles/stylish-chrome) and all was good. Then it ended.

Original creator of `Stylish` and `UserStyles.org` sold the project, and the new owner sold it again in 2017 to a web analytics company called Similar Web. Stylish extension was then used to literally steal all the browsing history of it's users. Every URL the user have opened, including all the keys in the URLs, together with their unique ID, and their IP address were in their entirety sent to their server. SimilarWeb knew everything about each of the `Stylish` users web activity, and never even asked the users for permission to collect it. 
In a forum post, they just wrote "Stylish users will be joining SimilarWeb’s market research panel". 

See this article for some details: https://robertheaton.com/2018/07/02/stylish-browser-extension-steals-your-internet-history/

In 2018, `Stylish` was removed from ChromeWebStore and the Firefox Addon Portal, and uninstalled from all user's browsers for stealing user data. 
After that, they got back, but this time they ask you for permission. 

They push for that permission quite hard (there are literally 11 colorful buttons to agree, in different languages), and also want you to create an account on userstyles.org. 
As they say in the extension: "We’re BEST at showing you styles for sites WHEN you visit them meaning we need access to that information. Meaning we're gonna need your agreement". 
From a Web Analytic company that sells data about people browsing habits, and used to steal that data, does that sound like a true statement? 
Lying about this breaches multiple laws and regulations regarding privacy. 

Although `userstyles.org` portal itself contains a lot of styles and is not as much of a threat, besides being a bit buggy, the permission-hungry, spywary `Stylish` extension is to be avoided, if you care about your privacy at all. 



In the context of the war for our attention, `Stylish` was one of the most popular tools that has been putting some control in the hands of the users. 
It was allowing them to alter the webpages, removing ads, feeds, and other annoyances with ease, for 11 years of the internet history, from 2005 up to 2016. 

It is quite ironic that such a tool was bought and destroyed by a company providing data for the advertisement industry. 
An industry which would very much like to see us without control over what we see on the web. 

They have won that particular battle, but they haven't won the war. 



There are alternatives for both the extension and the User Styles sharing portal. See below.

##### `Stylus` and `UserStyles.world` - a free and open source, community-managed fork of the `Stylish` extension, started from code before `Stylish` itself turned into spyware 

>  If you want to change the way that the internet looks, just use Stylus. It is functionally identical to Stylish, apart from the facts that it has never contained any spyware, and is not owned by a company that makes its money by selling your data. -- https://robertheaton.com/2018/08/16/stylish-is-back-and-you-still-shouldnt-use-it/















