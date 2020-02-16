---
layout: page
title: Austrian Medalists @ Winter Olympics 1980 - 2014
rdf_prefix_path: "_data/prefixes.sparql"
weight: 100
description: "Austrian Medalists @ Winter Olympics 1980 - 2014"
---

{% capture query %}

SELECT ?games ?year ?cityName
    WHERE {
        ?instance ex:games ?games . 
        ?games dbo:location ?city ;
        dbo:year ?year .
        ?city rdfs:label ?cityName .
    }
GROUP BY ?year ?cityName ?games 
ORDER BY DESC(?year)

{% endcapture %}
{% assign resultset = page.rdf | sparql_query: query %}

{% for result in resultset %}
<!-- {{ result.games }} -->
<div class="posts">
    <div>
        <a href="{{ result.games.page_url }}">{{ result.cityName}} {{ result.games | rdf_property: "dbo:year" }}</a>
    </div>
</div>
{% endfor %}
