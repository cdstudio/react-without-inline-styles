# Please stop using inline styles in [React](https://facebook.github.io/react/) components

It's a misconception.

## What are inline styles?

Inline styles are CSS styles written in javascript and added directly to a React Component. This trend started with the presentation [React: CSS in JS](https://speakerdeck.com/vjeux/react-css-in-js) and began spreading with introduction of [Radium](https://github.com/FormidableLabs/radium), which in fact tries to solve issues that appear when you start using inline styles. There is [a talk by Michael Chan](https://www.youtube.com/watch?v=ERB1TJBn32c) on why it's cool and (just a little) why it's not.

## Ok, what's wrong?

There is a number of issues that appear when you start using inline styles in an open source React Component that you want other people to use.

* For a markup person (knowing CSS and HTML but no JS) it will be very hard or impossible to change application style.
  * CSS was invented for styling. There is a lot of preprocessors (SASS, LESS, Stylus, PostCSS) that make it even better. Styling in javascript is wrong. Why don't we write React components in pure JS? Why did React developers invent JSX? Because declaring HTML DOM nodes is done best using HTML/XML syntax.
* It's almost always not overwritable.
  * If a component creator did inline styling only without allowing to overwrite it, it's impossible.
  * Component creator will 99% forget to allow overwriting component styles. I'm sure there will appear hundreds of projects which have inline styling and no ability to ovewrite it. It will apear. Because people may just forget to allow overwriting those styles. Someone will fill an issue. And later on mainatiner will add more functionality and will forget to allow overwriting it again. And this story begins over and over again.
  * If component creates self children automagically - you cannot overwrite children styles. There are projects that generate children inside a component with inline styling. Styles of children are just locked ([`material-ui`'s Menu](http://material-ui.com/#/components/menus) component)
* It's impossible to cross-mix. When using regular styles with classnames it's easy to mix styles from project1 with component from project2 (take `react-router`'s `<Link/>` styled with [google MDL](http://www.getmdl.io/)'s styles as an example). 

Using extrnal named styles just eliminates such issues from the very beginning. Developer has nothing to worry about and becomes a happy creator again ;) This is why I think inline styles approach has no future.

## What about modularity and dead style classes elimination?
* [Webpack](https://webpack.github.io/) allows to include CSS in a javascript file. This is just great! Just write your styles in CSS and include it inside of a component. This way you have only styles your current component uses and there is no longer dead styles problem, etc.

With webpack we can use not only CSS, but all those cool preprocessors like SASS, LESS, Stylus etc... [CSS-next](http://cssnext.io/) is my favorite. The coolest thing is that we can use all of them in a single project

  This manifesto was born from discussion on [gaearon/redux-devtools#37](https://github.com/gaearon/redux-devtools/issues/37)
  Please let me know if anyone already pointed some or all of this ideas elsewhere (I'm sure there should be such places).
