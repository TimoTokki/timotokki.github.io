---
layout: post
---

{{site.time}}

{% for page in site.pages %}
  path: {{ page.path }}
  
  id: {{ page.id }}
  
  url: {{ page.url }}
{% endfor %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

My first blog article.

{{ page.date | data_to_string }}