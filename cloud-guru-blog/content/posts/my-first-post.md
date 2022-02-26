---
title: "My First Post"
date: 2022-02-26T15:18:53+01:00
tags:
  - shortcodes
  - code blocks
  - mermaid
---

A simple example of bash block code:

```bash
echo "My first post with hugo"
```

An another example of terraform block code:

```terraform
resource "a_resource" "my_resource_name" {
  key = "value"
  anotherkey = "another value"
}
```

And finally, a graph with mermaid description:

{{< mermaid >}}
graph LR
  A-->B
  A-->C
  B-->D
  C-->D
{{< /mermaid >}}
