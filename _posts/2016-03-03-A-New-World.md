---
subtitle: often use it to try something new 
tag:
    - others
---

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

My first blog article.

{{ page.date | data_to_string }}