---
layout: post
tag:
    - jekyll
    - study notes

---

_config.yml


For technical reasons, this file is *NOT* reloaded automatically when you use 'jekyll serve'. If you change this file, please restart the server process.

<time></time> 是H5新标签，但未得到广泛应用

{{ post.content | strip_html | truncatewords:20}}

 | strip_html 是过滤器，过滤掉html标签;| truncatewords:20也是过滤器，限制字数



<!-- Side Catalog -->
{% if page.catalog %}
<script type="text/javascript">
    function generateCatalog (selector) {
        var post = $('div.post-container'),h,tagName,text,li,id,link;
        h = post.find('h1,h2,h3,h4,h5,h6');
        h.each(function () {
            tagName = $(this).prop('tagName').toLowerCase();
            id = "#"+$(this).prop('id');
            text = $(this).text();
            link = $('<a href="'+id+'" rel="nofollow">'+text+'</a>');
            li = $('<li class="'+tagName+'_nav"></li>').append(link);
            $(selector).append(li);
        });
        return true;    
    }

    generateCatalog(".catalog-body");

    // toggle side catalog
    $(".catalog-toggle").click((function(e){
        e.preventDefault();
        $('.side-catalog').toggleClass("fold")
    }))

    /*
     * Doc: https://github.com/davist11/jQuery-One-Page-Nav
     * Fork by Hux to support padding
     */
    async("{{ '/js/jquery.nav.js' | prepend: site.baseurl }}", function () {
        $('.catalog-body').onePageNav({
            currentClass: "active",
            changeHash: !1,
            easing: "swing",
            filter: "",
            scrollSpeed: 700,
            scrollOffset: 0,
            scrollThreshold: .2,
            begin: null,
            end: null,
            scrollChange: null,
            padding: 80
        });
    });
</script>
{% endif %}