---
image: img/Your-First-Blog-Post-1024x576.jpeg
title: "My First Post"
date: 2020-02-26T15:18:53+01:00
tags:
  - shortcodes
  - code blocks
  - mermaid
categories:
  - IaC
  - Archi
  - Code
---

A simple example of bash block code:

```bash {linenos=false}
echo "Date: $(date)"
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
