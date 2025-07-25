---
title: Add a hitmap on top of an image
slug: Web/HTML/How_to/Add_a_hit_map_on_top_of_an_image
page-type: how-to
sidebar: htmlsidebar
---

You can create a clickable image map in HTML using {{htmlelement('area')}} and {{htmlelement('map')}} elements.
This article describes how to set up an image map, and some downsides to consider before you build one.

<table>
<caption>Here are some things you need to know</caption>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        You should already know how to <a href="/en-US/docs/Learn_web_development/Getting_started/Your_first_website">create a basic HTML document</a> and how to <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images#how_do_we_put_an_image_on_a_webpage">add accessible images to a webpage.</a>
      </td>
    </tr>
    <tr>
      <th scope="row">Objective:</th>
      <td>
        Learn how to make different regions of one image link to different pages.
      </td>
    </tr>
  </tbody>
</table>

> [!WARNING]
> This article discusses client-side image maps only. Do not use server-side image maps, which require the user to have a mouse.

## Image maps, and their drawbacks

When you nest an image inside {{htmlelement('a')}}, the entire image links to one webpage. An image map, on the other hand, contains several active regions (called "hotspots") that each link to a different resource.

Formerly, image maps were a popular navigation device, but it's important to thoroughly consider their performance and accessibility ramifications.

> [!WARNING]
> Multiple images referencing the same image map may lead to unexpected browser behavior, severely degrading usability and accessibility. For example, when a user keyboard navigates an image with a re-used image map in Safari and Chromium-based browsers, latter image instances using that same image map are skipped entirely. In Firefox, all image maps get keyboard focus simultaneously and when the user keyboard navigates past the image, the next focused element is the one after the last image instance, effectively skipping everything between the two images.

[Text links](/en-US/docs/Learn_web_development/Core/Structuring_content/Creating_links) (perhaps styled with CSS) are preferable to image maps for several reasons: text links are lightweight, maintainable, often more SEO-friendly, and support accessibility needs (e.g., screen readers, text-only browsers, translation services).

## How to insert an image map, properly

### Step 1: The image

Not just any image is acceptable.

- The image must make it clear what happens when people follow image links. `alt` text is mandatory, of course, but many people never see it.
- The image must clearly indicate where hotspots begin and end.
- Hotspots must be large enough to tap comfortably, at any viewport size. How large is large enough? [72 × 72 CSS pixels is a good minimum,](https://uxmovement.com/mobile/finger-friendly-design-ideal-mobile-touch-target-sizes/) with additional generous gaps between touch targets. The map of the world at [50languages.com](https://www.goethe-verlag.com/book2/) (as of time of writing) illustrates the problem perfectly. It's much easier to tap Russia or North America than Albania or Estonia.

You insert your image [much the same way as always](/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images#how_do_we_put_an_image_on_a_webpage) (with an {{htmlelement("img")}} element and [`alt`](/en-US/docs/Web/HTML/Reference/Elements/img#alt) text). If the image is only present as a navigation device, you may write `alt=""`, provided you furnish appropriate [`alt`](/en-US/docs/Web/HTML/Reference/Elements/area#alt) text in the {{htmlelement('area')}} elements later on.

You will need a special [`usemap`](/en-US/docs/Web/HTML/Reference/Elements/img#usemap) attribute. Come up with a unique name, containing no spaces, for your image map. Then assign that name (preceded by a hash) as the value for the `usemap` attribute:

```html
<img src="image-map.png" alt="" usemap="#example-map-1" />
```

### Step 2: Activate your hotspots

In this step, put all your code inside a {{htmlelement('map')}} element. `<map>` only needs one attribute, the same map [`name`](/en-US/docs/Web/HTML/Reference/Elements/map#name) as you used in your `usemap` attribute above:

```html
<map name="example-map-1"> </map>
```

Inside the `<map>` element, we need {{htmlelement('area')}} elements. An `<area>` element corresponds to a single hotspot. To keep keyboard navigation intuitive, make sure the source order of `<area>` elements corresponds to the visual order of hotspots.

`<area>` elements are {{glossary("void element", "void elements")}}, but do require four attributes:

- [`shape`](/en-US/docs/Web/HTML/Reference/Elements/area#shape)
  - : The `shape` attribute takes one of four values: `circle`, `rect`, `poly`, and `default`. An `<area>` whose `shape` is `default` occupies the entire image, minus any other hotspots you've defined.
    If there is any overlap between the defined areas, the source order determines which area takes preference.
    The shape you choose determines the coordinate information you'll need to provide in `coords`.

- [`coords`](/en-US/docs/Web/HTML/Reference/Elements/area#coords)
  - : Coordinates are given in CSS pixels, and its value is dependent on the `shape` selected.
    - For a circle, provide the center's x and y coordinates, followed by the length of the radius.
    - For a rectangle, provide the x and y coordinates of the upper-left and bottom-right corners.
    - For a polygon, to provide the x and y coordinates of each corner (so, at least six values).

- [`href`](/en-US/docs/Web/HTML/Reference/Elements/area#href)
  - : The URL of the resource you're linking to. You may leave this attribute blank if you _don't_ want the current area to link anywhere (say, if you're making a hollow circle.)

- [`alt`](/en-US/docs/Web/HTML/Reference/Elements/area#alt)
  - : A mandatory attribute, telling people where the link goes or what it does. `alt` text only displays when the image is unavailable. Please refer to our [guidelines for writing accessible link text](/en-US/docs/Learn_web_development/Core/Structuring_content/Creating_links#use_clear_link_wording).

    You may write `alt=""` if the `href` attribute is blank _and_ the entire image already has an `alt` attribute.

```html
<map name="example-map-1">
  <area
    shape="circle"
    coords="200,250,25"
    href="page-2.html"
    alt="circle example" />

  <area
    shape="rect"
    coords="10, 5, 20, 15"
    href="page-3.html"
    alt="rectangle example" />
</map>
```

### Step 3: Make sure it works for everybody

You aren't done until you test image maps rigorously on many browsers and devices. Try following links with your keyboard alone. Try turning images off.

If your image map is wider than about 240px, you'll need to make further adjustments to make your website responsive. It's not enough to resize the image for small screens, because the coordinates stay the same and no longer match the image.

## Learn more

- {{htmlelement("img")}}
- {{htmlelement("map")}}
- {{htmlelement("area")}}
- [Online image map editor](https://www.maschek.hu/imagemap/)
