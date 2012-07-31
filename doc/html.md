[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation table of contents](README.md)

# The HTML

## Conditional `html` classes

A series of IE conditional comments apply the relevant IE-specific classes to
the `html` tag. This provides one method of specifying CSS fixes for specific
legacy versions of IE. While you may or may not choose to use this technique in
your project code, HTML5 Boilerplate's default CSS does not rely on it.

When using the conditonal classes technique, applying classes to the `html`
element has several benefits:

* It avoids a [file blocking
  issue](http://webforscher.wordpress.com/2010/05/20/ie-6-slowing-down-ie-8/)
  discovered by Stoyan Stefanov and Markus Leptien.
* It avoids the need for an empty comment that also fixes the above issue.
* CMSes like WordPress and Drupal use the body class more heavily. This makes
  integrating there a touch simpler.
* It still validates as HTML5.
* It uses the same element as Modernizr (and Dojo). That feels nice.
* It can improve the clarity of code in multi-developer teams.


## The `no-js` class

Allows you to more easily explicitly add custom styles when JavaScript is
disabled (`no-js`) or enabled (`js`). More here: [Avoiding the
FOUC](http://paulirish.com/2009/avoiding-the-fouc-v3/).


## The order of meta tags, and `<title>`

As recommended by [the HTML5
spec](http://www.whatwg.org/specs/web-apps/current-work/complete/semantics.html#charset)
(4.2.5.5 Specifying the document's character encoding), add your charset
declaration early (before any ASCII art ;) to avoid a potential
[encoding-related security
issue](http://code.google.com/p/doctype/wiki/ArticleUtf7) in IE. It should come
in the first [1024
bytes](http://www.whatwg.org/specs/web-apps/current-work/multipage/semantics.html#charset).

The charset should also come before the `<title>` tag, due to [potential XSS
vectors](http://code.google.com/p/doctype-mirror/wiki/ArticleUtf7).

The meta tag for compatibility mode [needs to be before all elements except
title and meta](http://h5bp.com/f "Defining Document Compatibility - MSDN").
And that same meta tag can only be invoked for Google Chrome Frame if it is
within the [first 1024
bytes](http://code.google.com/p/chromium/issues/detail?id=23003).


## X-UA-Compatible

This makes sure the latest version of IE is used in versions of IE that contain multiple rendering engines. Even if a site visitor is using IE8 or IE9, it's possible that they're not using the latest rendering engine their browser contains. To fix this, use:

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
```

The `meta` tag tells the IE rendering engine two things:

1. It should use the latest, or edge, version of the IE rendering environment
2. If already installed, it should use the Google Chrome Frame rendering
   engine.

This `meta` tag ensures that anyone browsing your site in IE is treated to the
best possible user experience that their browser can offer.

This line breaks validation, and the Google Chrome Frame part won't work inside
a conditional comment. To avoid these edge case issues it is recommended that
you **remove this line and use the `.htaccess`** (or other server config)
to send these headers instead. You also might want to read [Validating:
X-UA-Compatible](http://groups.google.com/group/html5boilerplate/browse_thread/thread/6d1b6b152aca8ed2).

If you are serving your site on a non-standard port, you will need to set this
header on the server-side. This is because the IE preference option 'Display
intranet sites in Compatibility View' is checked by default.


## Mobile viewport

The next key line that’s worth looking at is [the `viewport` meta tag](https://docs.google.com/present/view?id=dkx3qtm_22dxsrgcf4 "Viewport and Media Queries - The Complete Idiot's Guide"):

    <meta name="viewport" content="width=device-width">

There are a few different options that you can use with this meta tag. You can find out more in [the Apple developer docs](http://j.mp/mobileviewport).

## Favicons and Touch Icons

The shortcut icons should be put in the root directory of your site. The HTML5 Boilerplate comes with a default set of icons that you can use as a baseline to create yours.

If your site is in a sub-directory, make sure you add the `link` tags too so that the favicons can render as we noted in an [earlier version of this document](https://github.com/h5bp/html5-boilerplate/wiki/The-markup/5ab89f343a95483b068b22d8bbabaaffa3ad30fd).

## Modernizr

[Modernizr](http://modernizr.com) is a JavaScript library which hooks into the class attribute of the opening `html` tag (Line 2 in both versions of the Boilerplate), generates class names using feature detection, and sets up all browsers to properly render HTML5 elements.

(Wondering why the [HTML5 Shiv](https://code.google.com/p/html5shiv/) project, which uses JavaScript to fix the issues IE and others have with rendering HTML5, hasn’t been included in the boilerplate? The HTML5 Shiv is actually incorporated into Modernizr.)

HTML5 Boilerplate uses a custom build of Modernizr.

As well as improving HTML5 support, Modernizr also adds a series of class names to the `html` tag, where it initially says `no-js`, according to the browsers support for CSS3 and HTML5. This allows you to target parts of your CSS at only supporting browsers, leaving the rest to serve the plainer, albeit functional, version.

In general, in order to keep page load times to a minimum, it's best to call any JavaScript at the end of the page -- because if a script is slow to load from an external server, it may cause the whole page to hang. That said, the Modernizr script *needs* to run *before* the browser begins rendering the page, so that browsers lacking support for some of the new HTML5 elements are able to handle them properly. Therefore the Modernizr script is the only JavaScript file loaded at the top of the document.

## The content area

The central part of the boilerplate template is pretty much empty. This is intentional, in order to make the boilerplate suitable for both web page and web app development.

#### Google Chrome Frame

We finally have a Chrome Frame that [you do not need administrative rights to install](http://blog.chromium.org/2011/06/introducing-non-admin-chrome-frame.html). Because of this, we have included the prompt to install Chrome Frame by default for IE6 users. If you intend to support IE6, you should remove [this snippet](https://github.com/h5bp/html5-boilerplate/blob/93f0e38c510fdba16cbb68abe4dcfefa1f7034eb/index.html#L72-77).

### Google CDN for jQuery

Towards the bottom of the page we find the final few lines of code, beginning with the jQuery library. Regardless of which JavaScript library you use in your projects, it is well worth the time and effort to look up and reference the Google CDN (Content Delivery Network) version. Your users may already have this version cached in their browsers, and Google's CDN is likely far faster than your server. More on [[6,953 reasons why I still let Google host jQuery for me |http://encosia.com/2010/09/15/6953-reasons-why-i-still-let-google-host-jquery-for-me/]]

**Why not version `/1/` so you always get the latest version?**

The `/1/` version is [[only cached for 1 hour |http://paulirish.com/2009/caching-and-googles-ajax-libraries-api/]]. Also there can be breaking changes in jQuery 1.7 or whatever. You will want to deliberately upgrade your users.

**Note:** We load a protocol-independent absolute path of jQuery so you’re good to go on secure and non-secure pages. This works on all browsers as long as there is no redirection to a different URL after switching protocols. For more details on the technique, read [[The Protocol-relative URL |http://paulirish.com/2010/the-protocol-relative-url/]].

The following line provides the page with a fallback should the CDN version of the jQuery library not be available, likely only if you are offline or developing from a `file://` protocol. Some users report things being quite slow while developing locally (or via a fileserver) with the `//` URL; if it pains you too much, add in the `http:` to the URL. The `unescape` trick is necessary for using this snippet while in an XHTML environment, otherwise you could just do `document.write('<script src="js/jquery-1.4.4.min.js"><\/script>')`.

### Google Analytics Tracking Code

Finally, we get the latest version of the Google Analytics tracking code. This latest version includes a few new handy tricks from an analytics perspective, and also loads faster than the previous version. Google recommends that this script be placed at the top of the page. Factors to consider: if you place this script at the top of the page, you’ll be able to count users who don’t fully load the page, and you’ll incur the max number of simultaneous connections of the browser.

HTML5 Boilerplate 2.0 uses Yepnope to load the analytics script asynchronously. As mentioned earlier, if you intend to use
without Modernizr's custom build, read [Optimizing the asynchronous Google Analytics snippet](http://mathiasbynens.be/notes/async-analytics-snippet) and [Tracking Site Activity - Google Analytics](http://code.google.com/apis/analytics/docs/tracking/asyncTracking.html).
