---
author_profile: true
layout: splash
permalink: /
header:
  overlay_image: "assets/images/forest-deepdream.png"
  #cta_label: "<i class='fa fa-download'></i> Install Now"
  #cta_url: "/docs/quick-start-guide/"
  #caption:
excerpt: 'Personal site to keep public my computer science tryouts and experiments.
          Click [here](/year-archive/) to explore the posts.'
---
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %} `{{ tag }}` {% endfor %}
