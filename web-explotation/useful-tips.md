---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Useful Tips

Here we can find some tips for maximizing the use of web exploitation concepts, tools, and utilities:

* Check the URL for user information and queries, as well as the protocol being used.
* Make a map of routes to understand the flow of a website.
* Check general details such as the favicon, the _robots.txt_ file, and the _sitemap.xml_ file, among others.
* Check HTTP requests and responses, taking a view of specific details such as headers and their values.
* Check page source code (Use left click or go to the _view-source:$URL_ direction on the browser).
  * Check the code commentaries (`<!--`), anchors to other routes (`<a`), framework information, CSS scripts, and JS scripts.
* Check if URL parameters are displayed directly on the screen. This will tell us that a code injection can be done.
* Check if there are different errors in the forms.
  * If the username field of a login form shows a different error with specific entries, could mean that is an existing user.
* Check if token parameters are sent on the petitions.
* Modify HTML limit parameters in forms to input arbitrary values.
