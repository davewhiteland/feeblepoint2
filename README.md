# FeeblePoint2

* [See FeeblePoint2 running](https://davewhiteland.github.io/feeblepoint2/)

Single HTML page suitable for online presentations: jumps between "slides",
provides mouseover highlighting, and on-off big pointing cursors.

## Just one HTML page

If you quickly need to show something on your screen — maybe you're sharing
it in a call — and you want to be able to highlight or point at the things,
FeeblePoint2 might help.

## What it does

FeeblePoint2 is an HTML page which contains:

* SVG for a wee pointing hand, or ring, so you can indicate stuff on the screen

* CSS that does this:

  * treats `h2` headings as titles for slides (by throwing more than a
    screen-height of top-margin on them)...
  
  * provides single-letter classes that have (26) different colour on-hover
    highlights
  
  * manages the pointing device (including its colours)
  
  * anticipates a legend at the top of the page that shows which keys to press
    
  * general presentational stuff _which you should change_

* JavaScript that does this:

  * lets you "advance" through those slides (jumping from heading to heading)
    by giving each one a numeric id
  
  * it does this by updating the URL which is handy because it means bookmarks
    or browser-refresh behave helpfully if you need them to

  * adds event listeners for the key presses to make this happen
  
  * writes a header at the top of the page showing which keys to press

  * magically wraps words inside a `rainbow` class container with random colour
    on-hover `spans` (only simple content like words in headings or paragraphs)
    

You can disable the advance-as-slides, pointer, and legend features
independently. If you only want the pointing hand (it _is_ the best bit)
then just use that and disable the rest :-|

## How to use

Duplicate the `index.html`. Jump into your favourite text editor and delete the
existing "placeholder" HTML (there are clear comments in the HTML showing you
where that is), and put your own HTML presentation in there. Remember that
&lt;h2&gt; headings are (by default) the signifier of a slide.

If your favourite text editor doesn't have markdown-to-HTML capability to make
this simple then, uh, maybe you need to find a new favourite.

Maybe add HTML styling (there are classes like `a`, `b`, `c`, ...`z`) which do
highlighter colour on mouse-over (or `rainbow` to do a whole paragraph with
random colours).

If you want to change the behaviour of FeeblePoint2, the key features are
exposed as JavaScript constants to make this easier for you (see next section).


## Default keys (and how to change them)

You can change these by editing the JavaScript that's set up to make such
changes simple: this is from the JavaScript:

```javascript
//----------------------------------------------------------------------
//  FeeblePoint2     edit a few basic settings here, if you need to
//---------------------------------------------------------------------- 
// disable things by setting to false:
// if you disable a feature its keys settings will be ignored for you

const WANT_LEGEND_IN_HEADER         = true; // show keys at top of page?
const WANT_POINTER_ACTIONS          = true; // have pointer appear?
const WANT_SLIDE_NAVIGATION_ACTIONS = true; // jump between headings?

// change keys here!
//  - use "shift", "alt", "ctrl" and the keycode, separated by +
//  - case matters! (use the JavaScript keycode names)
//  - set a value to empty ("") to disable a single action
//  
//  examples: "KeyP", "Digit9", "ctrl+alt+shift+KeyZ"

const KEY_FOR_POINTER_FINGER = "KeyP";
const KEY_FOR_POINTER_RING   = "shift+KeyP";
const KEY_FOR_ADVANCE_SLIDE  = "Enter";
const KEY_FOR_BACK_SLIDE     = "KeyB";
const KEY_FOR_INDEX_SLIDE    = "Digit0";

const SLIDE_TAG = 'h2'; // If you change this, probably need to fix CSS too

// that's probably all you need to change
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

## Short history and tech notes

For nerds, [Feelblepoint](https://www.beholder.uk/feeblepoint/) was a way to
prepare an ignite talk, or things like ignite talks. It saw some action, but
these days you should use [reveal.js](https://revealjs.com) instead.

This one-pager (FeeblePoint2) has been handy for me, I hope it's handy for you too.
Being able to clearly indicate which part of the thing you're talking about
whilst sharing a screen on a "video call" or presentation seems to be a fairly
basic requirement.

The 26 single-letter highlighting classes are randomly associated with colours
— except `a` which is black (so won't work on my default (black background)
`code` styles). The highlight CSS uses `outline` (not `padding`) to be pretty
without risk of layout being affected.

The `rainbow` class is implemented in a *very* basic way so don't apply it to a
anything which itself contains tags. It really is just for simple paragraphs of
words or things like that. (TODO er maybe it should be better?)

If you're doing a _proper_ presentation, use [reveal.js](https://revealjs.com)
— a colleague has found it useful to drop the highlighting and pointer features
from FeeblePoint2 into those. Be sure to change the key mappings to not collide
with `reveal`. If you know what you're doing you can just paste in the bits of
code you want, but to make it a bit easier for you, the features can be
disabled (e.g., by setting `WANT_SLIDE_NAVIGATION_ACTIONS` to `false`) so you
don't have to pick out _bits_ of JavaScript to include.

If you change your "slide" heading from `h2` to some other tag, you'll need to
change the CSS that sets the big top-margin that throws each subsequent slide
below the page.

Note that the FeeblePoint2 JavaScript is adding `id` tags to all the `h2`
headings when the page loads: this may destroy any `id` tags that you had set.
If this is a problem (because you're using them as anchors for other links)
maybe move your anchors onto elements before the headings, so they are remain
untouched.

> Powerpoint is nearly always used for the convenience of the author,
> not the people at whom their presented is being fired. We can do better
> than that. Up with FeeblePoint and things like it!
>
> ![Feeblepoint Logo](https://camo.githubusercontent.com/acaf275db6bc1a973594051e06baa79933024da88acdb21546e762fa914ab35b/687474703a2f2f7777772e6265686f6c6465722e636f2e756b2f666565626c65706f696e742f64656d6f2f666565626c65706f696e742f666565626c65706f696e745f6c6f676f5f3230305f785f3132302e676966)

