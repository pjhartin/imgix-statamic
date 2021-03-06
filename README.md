![imgix logo](https://assets.imgix.net/imgix-logo-web-2014.pdf?page=2&fm=png&w=200&h=200)

# imgix-statamic

Easily generate imgix URLs inside Statamic.

**Please note that this release of `imgix-statamic` is designed for Statamic `v2.x`. If you are using Statmic `v1.x`, take a peek at [the version 1 releases](https://github.com/imgix/imgix-statamic/releases)**.

* [Installation](#installation)
* [Usage](#usage)
* [Meta](#meta)

<a name="installation"></a>
## Installation

1. Copy `site/addons/imgix` into your Statamic installation's `site/addons` folder.
2. Copy `site/settings/addons/imgix.yaml` into your Statamic installation's `site/settings/addons` folder.
3. Configure `imgix.yaml`:
    * `source` (Required): The imgix source domain to grab images from.
    * `secure_url_token`: Add this if you want to output signed (secure) image URLs.
    * `use_https`: Whether to use HTTPS URLs.
    * `responsive_resolutions`: The device pixel ratios used to generate `srcset` attributes.
4. Run `please addons:refresh` to install dependencies.


<a name="usage"></a>
## Usage

After you've installed and configured imgix-statamic, you can start using it in your Statamic templates! You can use [any available imgix parameter](https://www.imgix.com/docs/reference), including face detection, automatic format detection (WebP!), and more. Here are some examples to get you started:

### imgix:image_tag

The simplest way of working with imgix-statamic is using `imgix:image_tag`.

``` html
{{ imgix:image_tag path="dogs.png" w="200" rot="10" alt="Some dogs!" }}
```

Will output the following HTML:

``` html
<img src="https://your-source.imgix.net/dogs.png?w=200&rot=10" alt="Some dogs!">
```


### imgix:image_url

Makes it easy to generate an image URL in your site.

``` html
{{ imgix:image_url path="dogs.png" w="200" }}
```

Will output the following URL:

``` html
https://your-source.imgix.net/dogs.png?w=200
```


### imgix:responsive_image_tag

`imgix:responsive_image_tag` lets you easily add responsive images to your site.

`imgix:responsive_image_tag` will generate an `img` element with a filled-out `srcset` attribute that leans on imgix to do the hard work. It uses the configured device pixel ratios in the `responsive_resolutions` config variable (which defaults to `[1, 2]`). We talk a bit about using the srcset attribute in an application in the following blog post: [“Responsive Images with srcset and imgix”](http://blog.imgix.com/post/127012184664/responsive-images-with-srcset-imgix).

``` html
{{ imgix:responsive_image_tag path="dogs.png" w="200" }}
```

Will output the following HTML:

``` html
<img srcset="https://your-source.imgix.net/dogs.png?w=200 1x,
             https://your-source.imgix.net/dogs.png?w=200&dpr=2 2x"
     src="https://your-source.imgix.net/dogs.png?w=200">
```


### imgix:picture_tag

`imgix:picture_tag` simplifies adding `picture` elements to your site.

`imgix:picture_tag` will generate a `picture` element with a single `source` element and a fallback `img` element. It uses the configured device pixel ratios in the `responsive_resolutions` config variable (which defaults to `[1, 2]`).

``` html
{{ imgix:picture_tag path="dogs.png" w="200" alt="Some dogs!" }}
```

Will output the following HTML:

``` html
<picture>
    <source srcset="https://your-source.imgix.net/dogs.png?w=200 1x,
                    https://your-source.imgix.net/dogs.png?w=200&dpr=2 2x">
    <img src="https://your-source.imgix.net/dogs.png?w=200" alt="Some dogs!">
</picture>
```


#### Pass-through Attributes

Any imgix method that generates an `img` tag (`image_tag`, `responsive_image_tag`, and `picture_tag`) will automatically pass through the following attributes to the tag, if provided:

* `alt`
* `longdesc`
* `title`
* `data-*`
* `aria-*`


<a name="meta"></a>
## Meta

imgix-statamic was made by [imgix](http://imgix.com). It's licensed under the BSD 2-Clause license (see the [license file](https://github.com/imgix/imgix-statamic/blob/master/license.md) for more info).
