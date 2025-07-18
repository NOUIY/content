---
title: break-before
slug: Web/CSS/break-before
page-type: css-property
browser-compat: css.properties.break-before
sidebar: cssref
---

The **`break-before`** [CSS](/en-US/docs/Web/CSS) property sets how page, column, or region breaks should behave before a generated box. If there is no generated box, the property is ignored.

{{InteractiveExample("CSS Demo: break-before")}}

```css interactive-example-choice
break-before: auto;
```

```css interactive-example-choice
break-before: page;
```

```html interactive-example
<section id="default-example">
  <div>
    <p>
      The effect of this property can be noticed when the document is being
      printed or a preview of a print is displayed.
    </p>
    <button id="print-btn">Show Print Preview</button>
    <div class="box-container">
      <div class="box">Content before the property</div>
      <div class="box" id="example-element">Content with 'break-before'</div>
      <div class="box">Content after the property</div>
    </div>
  </div>
</section>
```

```css interactive-example
.box {
  border: solid #5b6dcd 5px;
  background-color: #5b6dcd;
  margin: 10px 0;
  padding: 5px;
}

#example-element {
  border: solid 5px #ffc129;
  background-color: #ffc129;
  color: black;
}

.hide-element {
  display: none;
}
```

```js interactive-example
const btn = document.getElementById("print-btn");
const editorContainer = document.getElementsByClassName(
  "css-editor-container",
)[0];
const exampleHTMLElement = document.getElementById("default-example");

const printableSection = document.createElement("div");
printableSection.setAttribute("id", "printable-section");
printableSection.classList.add("hide-element");
document.body.appendChild(printableSection);

btn.addEventListener("click", () => {
  const exampleContent = exampleHTMLElement.innerHTML;

  editorContainer.classList.add("hide-element");
  printableSection.innerHTML = exampleContent;
  printableSection.classList.remove("hide-element");

  window.print();

  printableSection.classList.add("hide-element");
  printableSection.innerHTML = "";
  editorContainer.classList.remove("hide-element");
});
```

## Syntax

```css
/* Generic break values */
break-before: auto;
break-before: avoid;
break-before: always;
break-before: all;

/* Page break values */
break-before: avoid-page;
break-before: page;
break-before: left;
break-before: right;
break-before: recto;
break-before: verso;

/* Column break values */
break-before: avoid-column;
break-before: column;

/* Region break values */
break-before: avoid-region;
break-before: region;

/* Global values */
break-before: inherit;
break-before: initial;
break-before: revert;
break-before: revert-layer;
break-before: unset;
```

Each possible break point (in other words, each element boundary) is affected by three properties: the {{cssxref("break-after")}} value of the previous element, the `break-before` value of the next element, and the {{cssxref("break-inside")}} value of the containing element.

To determine if a break must be done, the following rules are applied:

1. If any of the three concerned values is a _forced break value_ (`always`, `left`, `right`, `page`, `column`, or `region`), it has precedence. If more than one of them are such a break, the one of the element that appears the latest in the flow is taken (i.e., the `break-before` value has precedence over the `break-after` value, which itself has precedence over the `break-inside` value).
2. If any of the three concerned values is an _avoid break value_ (`avoid`, `avoid-page`, `avoid-region`, or `avoid-column`), no such break will be applied at that point.

Once forced breaks have been applied, soft breaks may be added if needed, but not on element boundaries that resolve in a corresponding `avoid` value.

### Values

#### Generic break values

- `auto`
  - : Allows, but does not force, any break (page, column, or region) to be inserted right before the principal box.
- `avoid`
  - : Avoids any break (page, column, or region) from being inserted right before the principal box.
- `always`
  - : Forces a page break right after the principal box. The type of this break is that of the immediately-containing fragmentation context. If we are inside a multicol container then it would force a column break, inside paged media (but not inside a multicol container) a page break.
- `all`
  - : Forces a page break right after the principal box. Breaking through all possible fragmentation contexts. So a break inside a multicol container, which was inside a page container would force a column and page break.

#### Page break values

- `avoid-page`
  - : Avoids any page break right before the principal box.
- `page`
  - : Forces a page break right before the principal box.
- `left`
  - : Forces one or two page breaks right before the principal box, whichever will make the next page into a left page. It's the page placed on the left side of the spine of the book or the back side of the page in duplex printing.
- `right`
  - : Forces one or two page breaks right before the principal box, whichever will make the next page into a right page. It's the page placed on the right side of the spine of the book or the front side of the page in duplex printing.
- `recto`
  - : Forces one or two page breaks right before the principal box, whichever will make the next page into a recto page. (A recto page is a right page in a left-to-right spread or a left page in a right-to-left spread.)
- `verso`
  - : Forces one or two page breaks right before the principal box, whichever will make the next page into a verso page. (A verso page is a left page in a left-to-right spread or a right page in a right-to-left spread.)

#### Column break values

- `avoid-column`
  - : Avoids any column break right before the principal box.
- `column`
  - : Forces a column break right before the principal box.

#### Region break values

- `avoid-region`
  - : Avoids any region break right before the principal box.
- `region`
  - : Forces a region break right before the principal box.

## Page break aliases

For compatibility reasons, the legacy {{cssxref("page-break-before")}} property should be treated by browsers as an alias of `break-before`. This ensures that sites using `page-break-before` continue to work as designed. A subset of values should be aliased as follows:

| page-break-before | break-before |
| ----------------- | ------------ |
| `auto`            | `auto`       |
| `left`            | `left`       |
| `right`           | `right`      |
| `avoid`           | `avoid`      |
| `always`          | `page`       |

> [!NOTE]
> The `always` value of `page-break-*` was implemented by browsers as a page break, and not as a column break. Therefore the aliasing is to `page`, rather than the `always` value in the Level 4 spec.

## Formal definition

{{cssinfo}}

## Formal syntax

{{csssyntax}}

## Examples

### Breaking into neat columns

In the following example we have a container that contains an `<h1>` spanning all columns (achieved using `column-span: all`) and a series of `<h2>`s and paragraphs laid out in multiple columns using `column-width: 200px`.

By default, the subheadings and paragraphs were laid out rather messily because the headings were not in a uniform place. However, we used `break-before: column` on the `<h2>` elements to force a column break before each one, meaning that you end up with an `<h2>` neatly at the top of each column.

#### HTML

```html
<article>
  <h1>Main heading</h1>

  <h2>Subheading</h2>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla vitae
    fringilla mauris. Quisque commodo eget nisi sed pretium. Mauris luctus nec
    lacus in ultricies. Mauris vitae hendrerit arcu, ac scelerisque lacus.
    Aliquam lobortis in lacus sit amet posuere. Fusce iaculis urna id neque
    dapibus, eu lacinia lectus dictum.
  </p>

  <h2>Subheading</h2>

  <p>
    Praesent condimentum dui dui, sit amet rutrum diam tincidunt eu. Cras
    suscipit porta leo sit amet rutrum. Sed vehicula ornare tincidunt. Curabitur
    a ipsum ac diam mattis volutpat ac ut elit. Nullam luctus justo non
    vestibulum gravida. Morbi metus libero, pharetra non porttitor a, molestie
    nec nisi.
  </p>

  <h2>Subheading</h2>

  <p>
    Vivamus eleifend metus vitae neque placerat, eget interdum elit mattis.
    Donec eu vulputate nibh. Ut turpis leo, malesuada quis nisl nec, volutpat
    egestas tellus.
  </p>

  <h2>Subheading</h2>

  <p>
    In finibus viverra enim vel suscipit. Quisque consequat velit eu orci
    malesuada, ut interdum tortor molestie. Proin sed pellentesque augue. Nam
    risus justo, faucibus non porta a, congue vel massa. Cras luctus lacus nisl,
    sed tincidunt velit pharetra ac. Duis suscipit faucibus dui sed ultricies.
  </p>
</article>
```

#### CSS

```css
html {
  font-family: helvetica, arial, sans-serif;
}

h1 {
  font-size: 3rem;
  letter-spacing: 2px;
  column-span: all;
}

h2 {
  font-size: 1.2rem;
  color: red;
  letter-spacing: 1px;
  break-before: column;
}

p {
  line-height: 1.5;
}

article {
  column-width: 200px;
  gap: 20px;
}
```

### Result

{{EmbedLiveSample('Breaking_into_neat_columns', '100%', 600)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Learn: Multiple-column Layout](/en-US/docs/Learn_web_development/Core/CSS_layout/Multiple-column_Layout)
- [Breaking Boxes With CSS Fragmentation](https://www.smashingmagazine.com/2019/02/css-fragmentation/)
