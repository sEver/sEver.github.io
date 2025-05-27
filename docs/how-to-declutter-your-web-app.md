# How to Declutter Your Web-App - Example Case with Trello.com

When we open the card in the Trello web app, we see "Comments and Activity" section on the right.
In that section, we have:

- "Write a Comment" field,
- and then below we have a list of comments with:
  - Avatar and Name of the commenter, dateTime of the comment,
  - Comment content
  - A row of Link-Buttons: Emoji+, Edit, [Add links as attachment], Delete

That row of links is absolutely destroying the flow of the section for the reader. No longer it is possible to just see all the comments, as you see both the metadata, and all possible actions with it.

Our aim will be to make the action-row appear only when the given comment is hovered.
Additionally, we will decrease the visibility of the dateTime part.

## Steps

### The downside of abandoning the CSS principles

It seems Trello is using a CSS preprocessor that takes from the developer the responsibility for managing the "width" of the CSS selectors. Instead of having logical system of CSS classess for the elements, the system is assigning a unique class to the elements, with their names auto-generated upon code "compilation".

Because of that, the class of our target action row is quite non descriptive: `<div class="PxL_3a0PSiOjGx">`

This will ofcourse change upon recompiling (so during any and all updates), and because of that, we cannot use that in our userStyle for selecting this block.

We will need to work around that.

### Selecting the comment

After opening the devtools and selecting the block encompassing entire single comment, we see that it is held within `<div class="X8WOA764yXoFYj" data-testid="card-back-action">`

Inside this block we have an unclassed `div` block with the avatar button, and a container block:

```html
<div class="Twu6_ppBo4S42z" data-testid="card-back-action-container"></div>
```

We can see that the "copy link to a comment" button appears next to the dateTime section, only after we hover this `card-back-action-container`, not the `card-back-action` one.

This is achieved by the following CSS code:

```css
.Twu6_ppBo4S42z:hover .FoWjYBy5S3qnJt {
  display: inline-block;
}
```

This block seems like a good place to hook our own action-row-hiding mechanic into.

We can target that container with the following code added to our userStyle with Stylus Browser Extension:

```css
div[data-testid="card-back-action-container"] {
  border: 1px solid red;
}
div:hover[data-testid="card-back-action-container"] {
  border: 1px solid green;
}
```

And then, we can add additional selectors for the parts that interest us:

```css
div[data-testid="card-back-action-container"] > div:first-child > span:nth-child(2) /* dateTime string */,
div[data-testid="card-back-action-container"] > div:first-child > div:nth-child(3) /* link icon */ {
  opacity: 0.5;
}
```

```css
div[data-testid="card-back-action-container"] > div:nth-child(3) /* action links row */ {
  display: none;
}
```
