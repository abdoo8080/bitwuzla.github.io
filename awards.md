---
layout: default
---

# Awards

{% assign years = site.data.awards.awards | map: "year" | uniq | sort | reverse %}
{% for year in years %}
{% assign yearStr = year | append: "" %}
{% assign yearInt = year | plus: 0 %}
{% assign entries = site.data.awards.awards | where_exp: "e","e.year == year" %}
{% for item in entries %}
<ul class="awards">
<li>
<b><a href="{{ item.event_url }}">{{ item.event }}</a></b> (<a href="{{ item.details | relative_url }}">details</a>)
<ul>
<li><span class="gray">entered:</span> {{ item.entered}} divisions</li>
<li><span class="gray">overall:</span>
{% assign gold = item.divisions.gold
  | plus: item.competition-wide.gold | plus: item.floc.gold %}
{% assign silver = item.divisions.silver
  | plus: item.competition-wide.silver | plus: item.floc.silver %}
{% assign bronze = item.divisions.bronze
  | plus: item.competition-wide.bronze | plus: item.floc.bronze %}
{% if gold > 0 %}<span class="awards">{{ gold }} gold medal{% if gold > 1 %}s{% endif %}</span>{% endif %}
{% if silver > 0 %}
  {% if gold > 0 %}, {% endif %}<span class="awards">{{ silver }} silver medal{% if silver > 1 %}s{% endif %}</span>
{% endif %}
{% if bronze > 0 %}
  {% if gold > 0 or silver > 0 %}, {% endif %}<span class="awards">{{ bronze }} bronze medal{% if bronze > 1 %}s{% endif %}</span>
{% endif %}
</li>
<li><span class="gray">division awards:</span>
  {{ item.divisions.gold }} gold medal{% if item.divisions.gold > 1 %}s{% endif %}
  (out of {{ item.divisions.total}})
</li>
{% if item.competition-wide %}
<li><span class="gray">competition-wide awards:</span>
  <ul>
  {% if item.competition-wide.gold > 0 %}
  <li>{{ item.competition-wide.gold }} gold medal{% if item.competition-wide.gold > 1 %}s{% endif %}
  (out of {{ item.competition-wide.total }})
  </li>
  {% endif %}
  {% if item.competition-wide.silver > 0 %}
  <li>{{ item.competition-wide.silver }} silver medal{% if item.competition-wide.silver > 1 %}s{% endif %}
  (out of {{ item.competition-wide.total }})
  </li>
  {% endif %}
  {% if item.competition-wide.bronze > 0 %}
  <li>{{ item.competition-wide.bronze }} bronze medal{% if item.competition-wide.bronze > 1 %}s{% endif %}
  (out of {{ item.competition-wide.total }})
  </li>
  {% endif %}
  </ul>
</li>
{% endif %}
{% if item.floc %}
<li><span class="gray">FLOC Olympic Games:</span>
  {% if item.floc.gold > 0 %}
    {{ item.floc.gold }} gold medal{% if item.floc.gold > 1 %}s{% endif %}
  {% endif %}
  {% if item.floc.silver > 0 %}
    {% if item.floc.gold > 0 %}, {% endif %}{{ item.floc.silver }} silver medal{% if item.floc.silver > 1 %}s{% endif %}
  {% endif %}
  {% if item.floc.bronze > 0 %}
    {% if item.floc.gold > 0 or item.floc.silver > 0 %}, {% endif %}{{ item.floc.bronze }} bronze medal{% if item.floc.bronze > 1 %}s{% endif %}
  {% endif %}
</li>
{% endif %}
</ul>
</li>
</ul>

{% endfor %}
{% endfor %}

