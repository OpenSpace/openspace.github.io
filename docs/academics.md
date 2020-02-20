---
title: Academics
layout: default

nav_order: 6
---

# Academics
Academic works that are related to OpenSpace.

1. TOC
{:toc}


## Papers
<ul>
{% assign sorted_papers = (site.papers | sort: 'date') | reverse %}
{% for paper in sorted_papers %}
  <li>
    {{paper.title}}, <i>{{paper.authors}}</i>, {{paper.journal}}, <b>{{paper.year}}</b>
    {% if paper.doi %}
    , <a href="{{paper.doi}}">{{paper.doi}}</a>
    {% endif %}
  </li>
{% endfor %}
</ul>

## Theses
<table>
  <tr>
    <th>Year</th>
    <th>Person</th>
    <th>Location</th>
    <th>Title</th>
    <th>Thesis</th>
  </tr>
{% assign sorted_theses = (site.theses | sort: 'date') | reverse %}
{% for thesis in sorted_theses %}
  <tr>
    <td>{{thesis.year}}</td>
    <td>{{thesis.name}}</td>
    <td>{{thesis.location}}</td>
    <td>{{thesis.title}}</td>
    {% if thesis.link %}
    <td><a href="{{thesis.link}}">link</a></td>
    {% else %}
    <td></td>
    {% endif %}
  </tr>
{% endfor %}
</table>
