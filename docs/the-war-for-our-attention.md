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

As we know - Mobile games are full of borderline gambling and well researched and tested psychological tricks, aiming to trigger addiction mechanism in their users.
They are widely known to have the most toxic, player-abusing systems in gaming, and in general are not liked that much for it. 
Yet still. Netflix chose to push them on us. 
There is no way to disable this behavior in netflix, no way to opt out of getting mobile games pushed onto you in your movie app. 

And unsurprisingly, [the users are outraged again](https://www.reddit.com/r/netflix/comments/1843gdv/disable_games/).



## Fighting back

Luckily for us, The Web was built upon standards and principles which did not leave us defenseless in the hands of corporations doing whatever they want to our information intake channels. 
Thanks to that, it is possible, and actually quite easy, to modify the behavior, shape, and content of the web apps we use. 

We can remove unwanted content and other annoyances from web apps, by modifying their code after the app code is loaded on our machine. 

There are a few ways to do that.  
1. The browsers Developer Tools can be used to modify the HTML/JS/CSS code of the app directly. (complex)
2. Dedicated Browser Extension that adds our own custom JS or CSS code to the webapp. (medium complexity, but quite versatile)
3. Dedicated Browser Extension that specifically targets the annoyances we want to remove. (easiest)



### 1. Modifying web-apps with Development Tools

In the past, there was an option to add custom user style CSS file to Google Chrome, which could override whatever we wanted on whatever page we wanted. 
This was the simplest single-file solution, but has since been disabled.

It is still possible to use Google Chrome DevTools to modify a file and add custom CSS to the target pages. 
This solution is relatively complex, and will be described in detail in a separate, future article.



### 2. Modifying web-apps with Browser Extension allowing us to add user-styles and user-scripts



#### The Case of Netflix Games

Let's use it as an example for how a user can fight back against products pushing on them things they'd rather not see. 

Hiding the abovementioned game-related content on netflix can be achieved by adding the following CSS code to the app.
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

div[data-list-context="popularTitles"].lolomoRow 
{
  margin-top: 5vw;
}

```

Now, to add this code to the web-app, we need a Browser Extension to add custom styles to the page. These custom styles are also known as `User Styles`.




#### What are User Styles? 

When CSS was being conceived, it was immediately obvious, that the author of a webpage can style it in a way that would not meet the needs or preferences of the user.

For this reason, the concept of a `User Style Sheet` was included in the design. 
A Style Sheet that can be defined by the User, to apply their own preferences to the web pages they were viewing. 

Take a look at the conformance specification of CSS (UAs in here means User Agents):
> UAs must allow users to specify a file that contains the user style sheet. UAs that run on devices without any means of writing or specifying files are exempted from this requirement. Additionally, UAs may offer other means to specify user preferences, for example, through a GUI. -- https://www.w3.org/TR/CSS2/conform.html#conformance

See some additional reference sources below:

https://www.w3.org/dpub/IG/wiki/User_Style_sheets

> CSS, or Cascading Style Sheets, offers a flexible way to style web content, with styles originating from browser defaults, **user preferences**, or web designers. [...] this separation maintains the **accessibility and readability of the content**, ensuring that the site is **usable for all users**, including those **with disabilities**. Its multi-faceted approach, including considerations for selector specificity, rule order, and media types, ensures that websites are visually coherent and **adaptive across different devices and user needs**, striking a balance between design intent and **user accessibility**. -- https://en.wikipedia.org/wiki/CSS#Sources // emphasis the author

> One of the goals of CSS is to **allow users greater control over presentation**. Someone who finds red italic headings difficult to read **may apply a different style sheet**. Depending on the browser and the website, **a user may choose from various style sheets provided by the designers, or may remove all added styles, and view the site using the browser's default styling, or may override just the red italic heading style without altering other attributes**. -- https://en.wikipedia.org/wiki/CSS#Sources // emphasis the author 

> If a page's layout information is stored externally, a **user can decide to disable the layout information entirely**, leaving the site's bare content still in a readable form. Site authors may also offer multiple style sheets, which can be used to completely change the appearance of the site without altering any of its content. Most modern web browsers also **allow the user to define their own style sheet**, which can include rules that **override the author's layout rules**. This allows users, for example, to bold every hyperlink on every page they visit. -- https://en.wikipedia.org/wiki/Style_sheet_(web_development)#Customization // emphasis by the author

> In order to **ensure that users can control styles**, CSS2 changes the semantics of the "!important" operator defined in CSS1. In CSS1, authors always had final say over styles. In CSS2, if a **user's style sheet** contains "!important", it **takes precedence** over any applicable rule in an author's style sheet. This is an important feature to users who require or must avoid certain color combinations or contrasts, users who require large fonts, etc. -- https://www.w3.org/1999/06/NOTE-CSS-access-19990616 // emphasis by the author

As we can see, the User's ability to override how a website (and therefore a web app) is displayed, is by design included within the very foundations of The Web. 
Firefox still respects that requirements, while Chromium used to, but stopped at some point, stating that this can be done with extensions. 

To extensions then we go.


#### Popular Browser Extensions for User Styles

This part needs a little history, as it seems people who embrace the core idea of the Web - that the user should have easy access to changing how the Web looks for them, are facing various difficulties on this path. 



##### Stylish and UserStyles.org - The first major `User Style Sheet` project, which after being sold, started stealing user data

While searching the web for "User Styles" You will most likely find in the top results: 
- `UserStyles.org` - a platform for publishing and sharing user styles.
- Browser Extension `Stylish` that has been downloaded by over 2'000'000 users. 

This pair was the User Style heaven for everyone, up until around 2016. 
An extension to apply custom styles to any web page, and a dedicated web portal used to share such custom styles with the entire world, with a searchable database of ready-to-use User Styles. 
A dream come true for the idea of user-customized web. The project was developed on GitHub (https://github.com/stylish-userstyles/stylish-chrome) and all was good. For a time.

Then it ended.



##### The Downfall of `Stylish` and `UserStyles.org`

In 2016, original creator of `Stylish` and `UserStyles.org` sold the project, and the new owner sold it again in 2017 to a web analytics company called Similar Web (or got employed by it, which is unclear). Stylish extension was then used to literally steal all the browsing history of it's over 2 million users. Every URL a user have opened, including all the keys in the URLs, all the custom "reset password" links, all the "only person with the link can access" links, everything together with their unique ID, and their IP address was in its entirety sent to the company server. SimilarWeb knew collected everything about each and every of the `Stylish` users web activity, without ever asking the users for permission to collect it. 
In a forum post, they just wrote "Stylish users will be joining SimilarWeb’s market research panel". 

See this article for some details: https://robertheaton.com/2018/07/02/stylish-browser-extension-steals-your-internet-history/

In response to the news about stealing user data, in July of 2018, 
`Stylish` extension was promptly removed from ChromeWebStore and the Firefox Addon Portal, and remotely uninstalled from all user's browsers. 

After about a month, they returned, again with a scheme to collect all the browsing data from their users, but this time they asked for permission. .

They ask for that permission quite hard as well, in a manipulative, coercive, misleading way. There are literally 11 colorful buttons to agree, in different languages. 
They also want you to create an account on userstyles.org, supposedly to better serve you the User Styles. 

As they say in the extension: "We’re BEST at showing you styles for sites WHEN you visit them meaning we need access to that information. Meaning we're gonna need your agreement". 
From a Web Analytic company that sells data about people browsing habits, and used to steal that data, that does not sound like a true statement. 
See how they make money: https://www.similarweb.com/corp/ourdata/
The user trust was already broken. Lying about this breaches multiple laws and regulations regarding privacy. They say one thing in the extension, but there something entirely different in the Privacy Policy on userstyles.org. It's a mess. 

Although `userstyles.org` portal itself contains a lot of styles and is not as much of a threat, besides being a bit buggy, 
the permission-hungry, spywary `Stylish` extension is best avoided, if you care about your privacy at all. 



In the greater context of the war for our attention, `Stylish` extension was one of the most popular tools that has been putting some control in the hands of the users. 
It was allowing them to alter the webpages, remove ads, feeds, and other annoyances with ease, for 11 years of the internet history, from 2005 up to 2016. 

It is quite ironic that such a tool was bought and destroyed by a company providing data for the advertisement industry. 
An industry which would very much like to see us without control over what we see on the web. 

They have won that particular battle, but they haven't won the war. 



There are alternatives for both the extension and the User Styles sharing portal. See below.



##### `Stylus` - a free and open source community-managed fork of the `Stylish` extension, started from code before `Stylish` itself turned into spyware 

This extension was a community response to the whole `Stylish` data stealing crisis. Redone with the single purpose - to continue providing the great usability that the original tool provided, but obviously without the whole spyware layer. 

>  If you want to change the way that the internet looks, just use Stylus. It is functionally identical to Stylish, apart from the facts that it has never contained any spyware, and is not owned by a company that makes its money by selling your data. -- https://robertheaton.com/2018/08/16/stylish-is-back-and-you-still-shouldnt-use-it/

The extension is available for both Chromium based browsers and Firefox, and has 800k users in total at the time of writing. 

- [Stylus page on ChromeWebStore](https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne) for Chromium based browsers (Chrome, Edge, Opera)
- [Stylus page on Mozzilla Firefox Addons](https://addons.mozilla.org/en-US/firefox/addon/styl-us/) for Firefox

There is also https://UserStyles.world portal, which enables publishing and downloading User Styles and is in no way connected to UserStyles.org

Since the entire value of UserStyles.org consists of User Styles added there by the users, to prevent the company owning it from deleting the User Styles history contained therein, all User Styles are mirrored onto https://uso.kkx.one/browse/styles and many authors import their User Styles from there into https://UserStyles.world

The crisis was averted, and users of The Web can again customize their web experience with ease and share the customizations. 



##### Using `Stylus` and `UserStyles.world` to remove annoyances from your web apps

Let's hide the game-related content on Netflix, as an example.

We need to:
0. Install the `Stylus` extension into our browser ([from here](https://chromewebstore.google.com/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne))
1. Install https://userstyles.world/style/22338/no-games-on-netflix
2. That's it! Now your Netflix doesn't show games.

**OR**

Manual process:
0. Install `Stylus` extension as above
1. Pin the extension to the toolbar (click the puzzle icon in top-right corner, find Stylus, and click the "Pin" icon)
3. Open https://netflix.com
4. Click the Stylus icon on the browser's toolbar
5. In the "Write new style for" section, uncheck "User CSS" blue checkbox
6. Click the "netflix.com" part of the url in this section
7. An editor window will open. Paste the code provided below into the big section on the right side of Stylus window
8. In the top-left corner enter a name for your User Style (Something like "Hiding Netlix Games")
9. Press Ctrl+S to save
10. And thats it. You've got a local User Style applied to your netflix.com. Now your Netflix doesn't show games.

```CSS

.billboard-row-games,
div[data-list-context="configbased_cloudpersonalizedgames"],
div[data-list-context="configbased_mobilepersonalizedgames"] 
{
  display: none;
}

div[data-list-context="popularTitles"].lolomoRow 
{
  margin-top: 5vw;
}

```



### 3. Dedicated browser extensions that specifically target annoyances we want to remove 
// To be expanded with ad blockers history and the `Manifest V2 vs V3` crisis, as well as Google deliberately lowering quality of their own search results.

Ad blockers such as UBlock Origin allow user-definable filters that can modify site's CSS.

- https://ublockorigin.com/ - the most powerful one, recently hurt by Google, together with many other ad-blocking tools, by "Manifest V3" set of changes to Extension system in Chromium. Google also disabled it on their ChromeWebStore.
- See also: https://cssi.us/manually-install-ublock-origin-in-chrome/















