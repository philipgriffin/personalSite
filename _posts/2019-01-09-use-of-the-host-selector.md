---
layout: post
title: Use of the :host selector
tags:
- 'Angular '
- CSS
excerpt_separator: "<!-- more -->"
date: 2019-01-09 13:13:52 +0000

---
The \`:host\`selector can be used to target custom components from within a css environment. Let's have a look!

<!-- more -->

Imagine you have a custom component such as;

\`\`\`html

<album></album>

\`\`\`

In your css you may want to style the album element from within it's inline stylesheet. 

This is where the \`:host\` selector comes in handy. Consider the below usage to add 10 pixels of margin to the album element.

\`\`\`

:host {

  margin: 10px;

}

\`\`\`