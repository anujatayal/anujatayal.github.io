---
layout: page
permalink: /news/
title: News
description: All news and announcements
nav: true
nav_order: 3
---

<!-- 
TO ADD NEW NEWS:
1. Edit _data/news_content.yml
2. Add a new entry in the 'news' array with:
   - date: "Your date format"
   - content: "Your news content"
   - year: YYYY (number)
3. The page will automatically update!
-->

<!-- HTML Structure Section -->
<div class="news">
  
  <style>
    .news-table th {
      width: 150px;
      min-width: 150px;
      white-space: nowrap;
      vertical-align: top;
      font-size: 0.9em;
      padding-right: 15px;
    }
    .news-table td {
      vertical-align: top;
    }
  </style>
  
  <div class="table-responsive">
    <table class="table table-sm table-borderless news-table">
      
      {% assign all_news = site.data.news_content.news | sort: "sort_date" | reverse %}
      {% assign years = all_news | map: "year" | uniq %}
      {% for year in years %}
        <!-- Year Header: {{ year }} -->
        <tr><td colspan="2"><h4 class="mt-4 mb-2">{{ year }}</h4></td></tr>
        
        {% assign year_news = all_news | where: "year", year %}
        {% for item in year_news %}
        <tr>
          <th scope="row" style="white-space: nowrap;">{{ item.date }}</th>
          <td>{{ item.content }}</td>
        </tr>
        {% endfor %}
      {% endfor %}
      
    </table>
  </div>
</div>
