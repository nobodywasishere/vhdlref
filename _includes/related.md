{%- assign tagEnableFlag = 0 -%}
{%- assign prevRef = "" -%}
{%- for refs in site.pages -%}
    {%- for pageTag in page.tags -%}
        {%- if refs.title != page.title and refs.tags contains pageTag and refs.title != prevRef -%}
            {%- if tagEnableFlag == 0 -%}
                <h2 id="see_also">
                    <a href="#see_also" class="anchor-heading" aria-labelledby="reference_manual">
                        <svg viewBox="0 0 16 16" aria-hidden="true">
                            <use xlink:href="#svg-link"></use>
                        </svg>
                    </a> See Also
                </h2>
                {%- assign tagEnableFlag = 1 -%}
                <ul>
            {%- endif -%}
            <li><a href="{{ site.baseurl }}/{{ refs.permalink }}">{{ refs.title }}</a></li>
            {%- assign prevRef = refs.title -%}
        {%- endif -%}
    {%- endfor -%}
{%- endfor -%}
</ul>
