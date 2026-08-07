---
layout: default
title: Home
---

# Daniel Kim

Cybersecurity student interested in penetration testing, security operations, network security, and cloud security.

This site documents my cybersecurity projects, technical notes, labs, and learning journey.

---

## Latest Posts

{% for post in site.posts %}

### [{{ post.title }}]({{ post.url | relative_url }})

**{{ post.date | date: "%B %d, %Y" }}**

{{ post.excerpt }}

[Read more →]({{ post.url | relative_url }})

---

{% endfor %}

## Areas I'm Learning

- Penetration Testing
- Vulnerability Assessment
- Network Security
- Linux & Windows Security
- Cloud Security
- Python
- Security Operations

## Connect

- [GitHub](https://github.com/santapower)
- [LinkedIn](https://www.linkedin.com/in/daniel-kim-489656329/)
