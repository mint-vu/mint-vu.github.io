---
title: People
permalink: /people/
---

{% assign people_sorted = site.people | sort: 'joined' %}
{% assign role_array = "pi|postdoc" | split: "|" %}

<div class="row">
  {% for role in role_array %}
    {% assign people_in_role = people_sorted | where: 'position', role %}
    {% if people_in_role.size == 0 %}
      {% continue %}
    {% endif %}

    <!-- Custom layout for PI and Postdocs -->
    {% if role == 'pi' or role == 'postdoc' %}
      <div class="column">
        <div class="pos_header">
          {% case role %}
            {% when 'pi' %}
              <h3>Principal Investigator</h3>
            {% when 'postdoc' %}
              <h3>Postdoctoral Fellows</h3>
          {% endcase %}
        </div>
    
        <div class="content list people">
          {% for profile in people_in_role %}
            <div class="list-item-people">
              <p class="list-post-title">
                {% if profile.avatar %}
                  <a href="{{ site.baseurl }}{{ profile.url }}"><img class="profile-thumbnail" src="{{site.baseurl}}/images/people/{{profile.avatar}}"></a>
                {% else %}
                  <a href="{{ site.baseurl }}{{ profile.url }}"><img class="profile-thumbnail" src="http://evansheline.com/wp-content/uploads/2011/02/facebook-Storm-Trooper.jpg"></a>
                {% endif %}
                <a class="name" href="{{ site.baseurl }}{{ profile.url }}">{{ profile.name }}</a>
              </p>
            </div>    
          {% endfor %}
        </div>
        <hr>
      </div>
    {% endif %}
  {% endfor %}
</div>
{% assign role_array = "gradstudent|researchstaff|visiting|undergrad|alumni" | split: "|" %}
{% for role in role_array %}

{% assign people_in_role = people_sorted | where: 'position', role %}

<!-- Skip section if there's nobody -->
{% if people_in_role.size == 0 %}
  {% continue %}
{% endif %}

<div class="pos_header">
{% if role == 'postdoc' %}
<h3>Postdoctoral Fellows</h3>
 {% elsif role == 'pi' %}
<h3>Principal Investigator</h3>
 {% elsif role == 'gradstudent' %}
<h3>Graduate Students</h3>
 {% elsif role == 'undergrad' %}
<h3>Undergraduate Students</h3>
 {% elsif role == 'researchstaff' %}
<h3>Research Staff</h3>
 {% elsif role == 'visiting' %}
<h3>Visiting Scholars</h3>
 {% elsif role == 'others' %}
<h3>Honorary Members</h3>
 {% elsif role == 'alumni' %}
<h3>Alumni</h3>
{% endif %}
</div>

{% if role != 'alumni' %}
<div class="content list people">
  {% for profile in people_sorted %}
    {% if profile.position contains role %}
      <div class="list-item-people">
        <p class="list-post-title">
          {% if profile.avatar %}
            <a href="{{ site.baseurl }}{{ profile.url }}"><img class="profile-thumbnail" src="{{site.baseurl}}/images/people/{{profile.avatar}}"></a>
          {% else %}
            <a href="{{ site.baseurl }}{{ profile.url }}"><img class="profile-thumbnail" src="http://evansheline.com/wp-content/uploads/2011/02/facebook-Storm-Trooper.jpg"></a>
          {% endif %}
          <a class="name" href="{{ site.baseurl }}{{ profile.url }}">{{ profile.name }}</a>
        </p>
      </div>    
    {% endif %}
  {% endfor %}
</div>
<hr>

{% else %}

<br>

| Who are they                                                 | When were they here               | Where they went                                              |
| :----------------------------------------------------------- | :-------------------------------- | :----------------------------------------------------------- |
| [Abihith Kothapalli](https://abi-kothapalli.github.io/) | Undergrad (Fall 2023-Spring 2025) | PhD Student in the Machine Learning Department at Carnegie Mellon University |
| [Kaiwen Shi](https://kwfredshi.github.io/) | Undergrad (Fall 2023-Spring 2025) | PhD Student in Computer Science, Vanderbilt University |
| [Rana Muhammad Shahroz Khan](https://www.linkedin.com/in/rana-m-shahroz/) | Undergrad (Fall 2022-Summer 2024) | PhD Student in the Computer Science Department at UNC        |
| [Zhanqi Zhu](https://www.linkedin.com/in/zhanqi-zhu/)        | Undergrad (Fall 2022-Summer 2024) | M.Sc. Student in the Computer Science Department at USC      |
| [Zihao (Harry) Zhu](https://www.linkedin.com/in/zihao-wu-a475ab262/) | Undergrad (Fall 2022-Summer 2023) | Master of Science Student in the Computer Science Department at Duke University |
| [Yuzhe (Bryan) Lu](https://www.linkedin.com/in/bryan-lu-419623180/) | Undergrad (Fall 2021-Summer 2022) | Master of Science Student in the Computer Science Department at CMU |

{% endif %}
{% endfor %}
