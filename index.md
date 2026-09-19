---
layout: default
---

<div class="home">
  {% assign posts_by_date = site.posts | group_by_exp: "post", "post.date | date: '%Y - %B'" %}
  
  {% if site.posts.size > 0 %}
    {% for group in posts_by_date %}
      <div class="post-group">
        <h3 class="post-group-heading">{{ group.name }}</h3>
        <ul class="post-list">
          {% for post in group.items %}
            <li class="post-item">
              <span class="post-date">{{ post.date | date: "%b %d" }}</span>
              <a class="post-link" href="{{ post.url | relative_url }}">
                {{ post.title }}
              </a>
            </li>
          {% endfor %}
        </ul>
      </div>
    {% endfor %}
  {% else %}
    <p>Nenhum post publicado ainda.</p>
  {% endif %}
</div>
