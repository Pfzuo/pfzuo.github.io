---
layout: default
permalink: /blog/
title: Blogs
nav: true
nav_order: 5
---

<div class="post">
  <div class="header-bar">
    <h1>{{ site.blog_name }}Welcome to Pengfei's Blog! 👏</h1>
    <h2>{{ site.blog_description }}</h2>
  </div>

  <div class="blog-list">
    {% assign latest_posts = site.posts | slice: 0, 3 %}
    {% for post in latest_posts %}
    <div class="blog-item">
      <h2 class="blog-title">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h2>
      {% if post.categories %}
      <div class="blog-meta">
        <span class="categories">
          {% for category in post.categories %}
          <span class="category">{{ category }}</span>
          {% endfor %}
        </span>
      </div>
      {% endif %}
      <div class="blog-excerpt">
        {% if post.excerpt %}
          {% assign paragraphs = post.excerpt | strip_html | split: ". " | slice: 0, 2 %}
          {% for paragraph in paragraphs %}
            <p>{{ paragraph }}.</p>
          {% endfor %}
        {% endif %}
      </div>
      <div class="post-info">
        <span class="date">{{ post.date | date: '%B %d, %Y' }}</span>
        {% assign words = post.content | strip_html | number_of_words %}
        <span class="reading-time">
          · {{ words | divided_by: 180 | plus: 1 }} min read
        </span>
      </div>
    </div>
    {% endfor %}
  </div>

  <div class="view-all">
    <a href="{{ '/archive/' | relative_url }}" class="view-all-link">View All Posts →</a>
  </div>
</div>

<style>
.post {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.header-bar {
  margin-bottom: 40px;
}

.header-bar h1 {
  font-size: 2em;
  margin-bottom: 10px;
  color: #333;  /* Dark color for light mode */
}

.header-bar h2 {
  font-size: 1.2em;
  font-weight: normal;
  color: #666;
}

.blog-list {
  margin-bottom: 40px;
}

.blog-item {
  margin-bottom: 40px;
  padding: 25px;
  border-radius: 8px;
  background-color: #f8f9fa;  /* Light gray background for the box */
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.blog-title {
  margin-bottom: 10px;
}

.blog-title a {
  color: #333;
  text-decoration: none;
  font-size: 0.9em;  
  font-weight: 900;
}

.blog-title a:hover {
  color: #b509ac;
}

.blog-meta {
  margin-bottom: 15px;
  color: #666;
  font-size: 0.9em;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 5px;
}

.blog-meta .date {
  margin-right: 15px;
}

.category {
  display: inline-block;
  margin-right: 10px;
  padding: 2px 8px;
  background: #f1f1f1;
  border-radius: 3px;
  font-size: 0.8em;
}

.blog-description {
  color: #444;
  line-height: 1.6;
}

.blog-excerpt {
  color: #444;
  line-height: 1.6;
  margin-top: 15px;
  font-size: 0.95em;
}

.blog-excerpt p {
  margin-bottom: 10px;
}

.view-all {
  text-align: center;
}

.view-all-link {
  display: inline-block;
  padding: 10px 20px;
  color: #0366d6;
  text-decoration: none;
  font-weight: 500;
}

.view-all-link:hover {
  text-decoration: underline;
}

.reading-time {
  color: #666;
}

/* Dark mode updates */
@media (prefers-color-scheme: dark) {
  .blog-title a {
    color: #e6e6e6;
  }

  .blog-title a:hover {
    color: #58a6ff;
  }

  .blog-meta {
    color: #888;
  }

  .blog-description {
    color: #ccc;
  }

  .category {
    background: #2d2d2d;
  }

  .blog-item {
    background-color: #1a1a1a;
    border: 1px solid #333;
    box-shadow: 0 1px 3px rgba(0,0,0,0.2);
  }
  
  .view-all-link {
    color: #58a6ff;
  }

  .blog-excerpt {
    color: #333 !important;  
  }

  .p {
    color: #333 !important;  
  }

  .post-info {
    color: #333;
  }

  .reading-time {
    color: #333 !important;
  }

  .date {
    color: #333 !important;
  }

  .header-bar h1 {
    color: #fff !important;
  }
}
</style>