---
layout: default
title: Home
---

# Daniel Kim

## Cybersecurity Engineer

I’m a cybersecurity professional pursuing a B.S. in Cybersecurity at Purdue University.

My interests include penetration testing, security operations, networking, and cloud security.

I’m also interested in AI security, secure AI systems, and AI guardrails.

---

## Latest Post

{% assign latest_post = site.posts.first %}

{% if latest_post %}

### [{{ latest_post.title }}]({{ latest_post.url | relative_url }})

**{{ latest_post.date | date: "%B %d, %Y" }}**

{% if latest_post.description %}
{{ latest_post.description }}
{% endif %}

[Read more →]({{ latest_post.url | relative_url }})

{% endif %}
