---
layout: default
permalink: /archive/
title: Archives
nav: true
nav_order: 25
---

<div class="archive">
  {% assign postsByYear = site.posts | group_by_exp:"post", "post.date | date: '%Y'" %}
  
  {% for year in postsByYear %}
    <h2 class="archive-year" id="{{ year.name }}">{{ year.name }}</h2>
    <ul class="archive-list">
      {% for post in year.items %}
        <li class="archive-item">
          <span class="archive-date">{{ post.date | date: "%Y-%m-%d" }}</span>
          <a href="{{ post.url | relative_url }}" class="archive-title">{{ post.title }}</a>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<style>
.archive {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.archive-year {
  margin-top: 30px;
  border-bottom: 2px solid #eee;
  padding-bottom: 10px;
}

.archive-list {
  list-style: none;
  padding-left: 0;
}

.archive-item {
  margin: 10px 0;
  display: flex;
  align-items: baseline;
}

.archive-date {
  color: #666;
  font-size: 0.9em;
  min-width: 100px;
  margin-right: 20px;
}

.archive-title {
  text-decoration: none;
  color: #333;
}

.archive-title:hover {
  color: #b509ac;
}

/* 暗色主题样式 */
@media (prefers-color-scheme: dark) {
  .archive {
    background-color: #1a1a1a;
  }

  .archive-year {
    color: #fff;
    border-bottom-color: #333;
  }

  .archive-date {
    color: #888;
  }

  .archive-title {
    color: #e6e6e6;
  }

  .archive-title:hover {
    color: #2698ba;
  }
}
</style>