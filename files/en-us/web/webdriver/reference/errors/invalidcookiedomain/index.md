---
title: Invalid cookie domain
slug: Web/WebDriver/Reference/Errors/InvalidCookieDomain
page-type: webdriver-error
sidebar: webdriver
---

The **invalid cookie domain** error is a [WebDriver error](/en-US/docs/Web/WebDriver/Reference/Errors) that occurs when an illegal attempt was made to set a [cookie](/en-US/docs/Glossary/Cookie) under a different [domain](/en-US/docs/Glossary/Domain) than that of the current document.

In WebDriver it is not permissible to set cookies for other domains than the domain of the [current browsing context](/en-US/docs/Glossary/Browsing_context)'s [document](/en-US/docs/Web/API/Document)'s domain.

This error will also happen if the document is _cookie-averse_, that is if the document is not loaded via `http://`, `https://`, or `ftp://`.

## Example

### Other domains

If the current domain were to be `example.com`, it would not be possible to [add a cookie](/en-US/docs/Web/WebDriver/Reference/Commands/AddCookie) for the domain `example.org`:

```python
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
session.get("https://example.com/")
try:
    cookie = {"name": "foo",
              "value": "bar",
              "domain": "example.org"}
    session.add_cookie(cookie)
except exceptions.InvalidCookieDomainException as e:
    print(e.message)
```

Output:

```plain
InvalidCookieDomainException: https://example.org/
```

### Cookie-averse documents

This error may also occur when you visit a cookie-averse document, such as a file on your local disk:

```python
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
session.get("file:///home/jdoe/document.html")
try:
    foo_cookie = {"name": "foo", "value": "bar"}
    session.add_cookie(foo_cookie)
except exceptions.InvalidCookieDomainException as e:
    print(e.message)
```

Output:

```plain
InvalidCookieDomainException: Document is cookie-averse
```

## See also

- [List of WebDriver errors](/en-US/docs/Web/WebDriver/Reference/Errors)
- Relevant WebDriver commands:
  - [Add Cookie](/en-US/docs/Web/WebDriver/Reference/Commands/AddCookie)
  - [Delete Cookie](/en-US/docs/Web/WebDriver/Reference/Commands/DeleteCookie)
  - [Delete All Cookies](/en-US/docs/Web/WebDriver/Reference/Commands/DeleteAllCookies)
  - [Get All Cookies](/en-US/docs/Web/WebDriver/Reference/Commands/GetAllCookies)
  - [Get Named Cookie](/en-US/docs/Web/WebDriver/Reference/Commands/GetNamedCookie)
