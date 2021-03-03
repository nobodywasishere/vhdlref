{% assign crsize = page.used-in | size %}
{% if crsize != 0 %}
<h2 id="used_in">
    <a href="#used_in" class="anchor-heading" aria-labelledby="reference_manual">
        <svg viewBox="0 0 16 16" aria-hidden="true">
            <use xlink:href="#svg-link"></use>
        </svg>
    </a> Used In
</h2>
<ul>
    {% for cr in page.used-in %}
        <li>{{ cr }}</li>
    {% endfor %}
</ul>
{% endif %}

{% if page.lrm %}
<h2 id="reference_manual">
    <a href="#reference_manual" class="anchor-heading" aria-labelledby="reference_manual">
        <svg viewBox="0 0 16 16" aria-hidden="true">
            <use xlink:href="#svg-link"></use>
        </svg>
    </a> Reference Manual
</h2>
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
