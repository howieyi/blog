---
layout: page
title: Linux 日常涉猎
permalink: /linux
---

## Linux 日常涉猎

{% for item in site.data.linux %}
### [{{ item.name }}]({{site.baseurl}}{{ item.link }})
{% endfor %}