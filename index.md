# Daniel Kim

## Cybersecurity Engineer

I’m a cybersecurity professional pursuing a B.S. in Cybersecurity at Purdue University, with experience in cybersecurity, software development, and networking.

### I’m interested in:

- Penetration Testing
- Security Operations
- Network & Cloud Security
- AI Security & Secure AI Systems
- AI Guardrails

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

---

## Connect

[LinkedIn](https://www.linkedin.com/in/daniel-kim-489656329/) · [GitHub](https://github.com/santapower)
