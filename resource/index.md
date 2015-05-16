---
layout: home
---

<div class="index-content resource">
    <div class="section">
        <ul class="artical-cate">
          <li ><a href="/blog"><span>官方出版</span></a></li>
          <li style="text-align:center"><a href="/member_blog"><span>分享延伸</span></a></li>
          <li class="on" style="text-align:right" ><a href="/resource"><span>常用资源</span></a></li>
        </ul>
        <div class="cate-bar"><span id="cateBar"></span></div>

        <ul class="artical-list">
        {% for post in site.categories.resource %}
            <li>
                <h2>
                    <a href="{{ post.url }}">{{ post.title }}</a>
                </h2>
                <div class="title-desc">{{ post.description }}</div>
            </li>
        {% endfor %}
        </ul>
    </div>
    <div class="aside">
    </div>
</div>
