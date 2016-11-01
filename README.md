# testament-megadropdown-for-mobile
Testament theme - add the mega dropdown into the mobile menu

Open: theme.liquid and between lines: 130 - 159
You will see this:

```html
<div id="dl-menu" class="dl-menuwrapper">
    <button class="dl-trigger"><i class="icon-align-justify"></i></button>
    <ul class="dl-menu">

      {% for link in linklists.main-menu.links %}
      <li {% capture child_list_handle %}{{ link.title | handleize }}{% endcapture %}{% if linklists[child_list_handle] and linklists[child_list_handle].links.size > 0 %}{% endif %}>
        {{ link.title | link_to: link.url }}
        {% capture child_list_handle %}{{ link.title | handleize }}{% endcapture %}
        {% if linklists[child_list_handle] and linklists[child_list_handle].links.size > 0 %}       
        <ul class="dl-submenu">
          {% for l in linklists[child_list_handle].links %}
          <li><a href="{{ l.url }}">{{ l.title }}</a>

            {% capture child_list_handle %}{{ l.title | handleize }}{% endcapture %}
            {% if linklists[child_list_handle] and linklists[child_list_handle].links.size > 0 %}       
            <ul class="dl-submenu">
              {% for l in linklists[child_list_handle].links %}
              <li><a href="{{ l.url }}">{{ l.title }}</a></li>
              {% endfor %}
            </ul>
            {% endif %}

          </li>
          {% endfor %}
        </ul>
        {% endif %}
      </li>
      {% endfor %}
    </ul>
  </div><!-- /dl-menuwrapper -->  
  ```
  
  Replace it with this:
  
```html
<div id="dl-menu" class="dl-menuwrapper">
    <button class="dl-trigger"><i class="icon-align-justify"></i></button>
    <ul class="dl-menu">

      {% for link in linklists.main-menu.links %}
      
      {% if link.title == settings.megadropdown_link %}
      <li>{{ link.title | link_to: link.url }}
      <ul class="dl-submenu">

        {% assign mega = 0 %}
        {% if settings.mega_1_show %}{% assign mega = mega | plus: 1 %}{% endif %}
        {% if settings.mega_2_show %}{% assign mega = mega | plus: 1 %}{% endif %}
        {% if settings.mega_3_show %}{% assign mega = mega | plus: 1 %}{% endif %}
        {% if settings.mega_4_show %}{% assign mega = mega | plus: 1 %}{% endif %}

        {% if mega > 0 %}    
        <!-- Start Megamenu Inner Links -->
        {% if settings.mega_1_show %}            
        <li><a href="#">{{ linklists[settings.mega_1_links].title }}</a>
          <ul class="dl-submenu">
            {% for link in linklists[settings.mega_1_links].links %}
            <li>{{ link.title | link_to: link.url }}</li>
            {% endfor %}
          </ul>
        </li>
        {% endif %}
        {% if settings.mega_2_show %}            
        <li><a href="#">{{ linklists[settings.mega_2_links].title }}</a>
          <ul class="dl-submenu">
            {% for link in linklists[settings.mega_2_links].links %}
            <li>{{ link.title | link_to: link.url }}</li>
            {% endfor %}
          </ul>
        </li>
        {% endif %}
        {% if settings.mega_3_show %}            
        <li><a href="#">{{ linklists[settings.mega_3_links].title }}</a>
          <ul class="dl-submenu">
            {% for link in linklists[settings.mega_3_links].links%}
            <li>{{ link.title | link_to: link.url }}</li>
            {% endfor %}
          </ul>
        </li>
        {% endif %}
        {% if settings.mega_4_show %}            
        <li><a href="#">{{ linklists[settings.mega_4_links].title }}</a>
          <ul class="dl-submenu">
            {% for link in linklists[settings.mega_4_links].links %}
            <li>{{ link.title | link_to: link.url }}</li>
            {% endfor %}
          </ul>
        </li> 
        {% endif %}    
        {% endif %}     

      </ul>

      </li>

    {% else %}      
      
      
      <li {% capture child_list_handle %}{{ link.title | handleize }}{% endcapture %}{% if linklists[child_list_handle] and linklists[child_list_handle].links.size > 0 %}{% endif %}>
        {{ link.title | link_to: link.url }}
        {% capture child_list_handle %}{{ link.title | handleize }}{% endcapture %}
        {% if linklists[child_list_handle] and linklists[child_list_handle].links.size > 0 %}       
        <ul class="dl-submenu">
          {% for l in linklists[child_list_handle].links %}
          <li><a href="{{ l.url }}">{{ l.title }}</a>

            {% capture child_list_handle %}{{ l.title | handleize }}{% endcapture %}
            {% if linklists[child_list_handle] and linklists[child_list_handle].links.size > 0 %}       
            <ul class="dl-submenu">
              {% for l in linklists[child_list_handle].links %}
              <li><a href="{{ l.url }}">{{ l.title }}</a></li>
              {% endfor %}
            </ul>
            {% endif %}

          </li>
          {% endfor %}
        </ul>
        {% endif %}
      </li>
      {% endif %}
      {% endfor %}
    </ul>
  </div><!-- /dl-menuwrapper -->  
    ```
    
    click save when done + test the menu.
