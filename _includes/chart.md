{% assign crsize = page.used-in | size %}
{% if crsize != 0 %}
<h2>Used In</h2>
<ul>
    {% for cr in page.used-in %}
        <li>{{ cr }}</li>
    {% endfor %}
</ul>
{% endif %}

<h2>Reference Manual</h2>

{% if page.lrm %}
    {% for lrm in page.lrm %}
        {% for version in lrm %}
            {% for section in version %}
                {% if forloop.first %}
                    VHDL-{{ section }}:
                    <ul>
                {% else%}
                    {% for indv in section %}
                    <li>Section {{ indv }}</li>

                    {% endfor %}
                {% endif %}
                {% if forloop.last %}
                    </ul>
                {% endif %}
            {% endfor %}
        {% endfor %}
    {% endfor %}
{% endif %}
