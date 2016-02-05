# CSS Manifests

## Objectives

1. Create CSS Manifest Files
2. Require CSS Files in Manifests with Sprocket Directives
3. Include CSS Manifest Files in Layouts
4. See a Manifest in Development vs Production

## Outline
CSS makes our web applications look good but can be hard to manage. As our application grow, so does the amount of styles we need. Asset pipeline can help us manage this chaos much like with JavaScript.

### Manifest Files

Much like our JavaScript manifest, the CSS manifest has a special syntax that differentiates it from a regular CSS file. The `*= require` directive is very similiar to it's JS conterpart but instead is found inside of a CSS comment.

```
/*
*= require 'main'
*/
```

_Note_: In a CSS manifest file you must open the CSS comment block with `/*` and then each directive appears on an individual line starting with `*=`. You close the comment block with `*/`. It's a little different than the JS directive comments of `//=` which are individual valid JS comments.

### `require` directives

The `require` directive 
Remember that when you require something the path you provide must be the asset path, as though accessed via /assets

### Loading a Manifest File in your layout

Loading our CSS manifest file into our application is just as easy as it was with JS. We create a `stylesheet_link_tag` in our application layout and Sprockets takes care of loading the manifest and determining what assets to include.

```erb
<%= stylesheet_link_tag 'application' %>
```

In development mode, each CSS file will get it's own link tag. This allows for easier debugging. A manifest file that looks like this:

```css
/*
*= require 'main'
*= require 'blogs'
*= require 'posts'
*/
```

Would create this in our application layout's head tag:

```html
  <link rel="stylesheet" href="/assets/main.css" /> 
  <link rel="stylesheet" href="/assets/blogs.css" /> 
  <link rel="stylesheet" href="/assets/posts.css" /> 
```

#### Manifests in Production
In production mode, Sprockets will take all of our CSS files and create one large CSS file. It will also minify the contents removing unneeded whitespace to reduce the overall size of the file. Both of these features will speed up page loads for our users. If we look at our previous manifest example:

```css
/*
*= require 'main'
*= require 'blogs'
*= require 'posts'
*/
```

We would only get a single link tag from this in our application manifest.

```html
<link rel="stylesheet" href="/assets/application-4dd5b109ee3439da54f5bdfd78a80473.css" /> 
```
The end result looks like this:
```css
body{background-color:#FFF;font-size:14px;margin:0}a{color:#1B97F2;text-decoration:none}.clear{clear:both}ul{margin:4px 0;padding-left:17px}ul.horizontal{list-style:none;margin:0;padding:0}ul.horizontal li{margin:0;padding:0;float:left}#flash_notice,#flash_alert{padding:10px 0;text-align:center;color:#FFF}
```
Notice the lack of whitespace? That's the minification we taked about earlier. This is great for production use but you probably noticed it's a bit hard to read. This is why when we are in development we get individual unminified files instead of this.

## Resources
- https://github.com/rails/sprockets#sprockets-directives
- http://guides.rubyonrails.org/asset_pipeline.html

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/css-manifests' title='CSS Manifests'>CSS Manifests</a> on Learn.co and start learning to code for free.</p>
