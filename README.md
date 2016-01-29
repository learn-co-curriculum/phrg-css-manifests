# CSS Manifests

## Objectives

1. Create CSS Manifest Files
2. Require CSS Files in Manifests with Sprocket Directives
3. Include CSS Manifest Files in Layouts
4. See a Manifest in Development vs Production

## Outline

### Manifest Files

There are two things that make a CSS file in app/assets a manifest file as opposed to actual CSS code.

1. You load it into a main layout via stylesheet_link_tag

2. You use the magic "sprocket" directives that are valid CSS comments that look like:

```
/*
*= require 'main'
*/
```

_Note_: In a CSS manifest file you must open the CSS comment block with `/*` and then each directive appears on an individual line starting with `*=`. You then close the block with `*/`. So it's a little different than the JS directive comments of `//=` which are individual valid JS comments.

### `require` directives

Let's learn about the directives available to you to require files into a manifest.

https://github.com/rails/sprockets#sprockets-directives

The most common one is require and in fact we recommend explicitly loading asset dependencies using only require. require_tree and the such can lead to weird issues with load order and dependencies.

Remember that when you require something the path you provide must be the asset path, as though accessed via /assets

### Loading a Manifest File in your layout

Nothing special here, when you say stylesheet_link_tag it will see if it's a manifest an act accordingly loading all the dependencies or it will simply create a style link tag for the single CSS file.

When you see stylesheet_link_tag application you think 1 file was loaded but actually many were.

Show the student that there is a style link tag for each file in the manifest.

Show how to debug manifest files that require files that can't be found.

#### Manifests in Production

Show what a concatenated manifest looks like in production.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/css-manifests' title='CSS Manifests'>CSS Manifests</a> on Learn.co and start learning to code for free.</p>
