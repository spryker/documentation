Given that we are working on a web application, we need a proper way to generate HTML dynamically. The most common approach relies on templates and for this we decided to go with Twig Template Engine.

@(Info)()(You can use other technology for the front-end of your application as well; this is just a recommendation and this is what we used for building Demoshop's front-end.)

<details open>
<summary>Click here to view a typical twig layout template</summary>
    
```
<!DOCTYPE html>
<html>
    <head>
        <title>{{ page_title }}</title>

        {% block header_css %}
        <link href="/path/to/bootstrap.min.css" rel="stylesheet" />
        {% endblock %}
    </head>
    <body>
        <h1>{{ page_title }}</h1>

        <ul id="navigation">
            {% for item in navigation %}
                <li><a href="{{ item.url }}">{{ item.label }}</a></li>
            {% endfor %}
        </ul>

        <div class="container">
            {% block body %}
            <div class="row">
                <div class="col-md-3">
                    {% include 'partial/sidebar.twig' %}
                </div>
                <div class="col-md-9">
                    {% block body %}
                        {# This block should always come from the page template
                        which extends this layout file. #}
                    {% endblock %}
                </div>
            </div>
            {% endblock %}
        </div>

        {% block footer_js %}
        <script src="/path/to/compiled-and-combined-js-files.js"></script>
        {% endblock %}
    </body>
</html>
```
    
</br>
</details>

</br>

For more information, see [Best Practices - Twig Templates](https://documentation.spryker.com/v4/docs/twig-best-practices). 

## Markup Tags

Twig has 3 specific markup tags:

1. comment tag
2. print tag
3. block tag

### Comment tag
When using the comment tag, the content is not rendered to the output HTML.

```bash
{# comments are not rendered #}

{# comments
can be
on multiple lines
as well
#}
```

### Print tag

Prints the given expression similar to  <?php echo

```
{{ variable_name }}

{{ 'print me!' }}
```

### Block tag
Used mostly for control-flow statements like if, for, include, block, set
if you are doing something and not printing something, use this tag:

```
{% set foo = 'bar' %}

{% if foo is 'bar' %}
...
{% endif %}
```

**See also:**
[Twig Homepage](https://twig.symfony.com/)
