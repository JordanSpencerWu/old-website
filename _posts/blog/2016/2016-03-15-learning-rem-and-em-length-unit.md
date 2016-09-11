---
categories: [blog]
date: 2016-03-15 13:15:00
layout: post
title: "Learning rem and em Length Unit"
---
<article class="module" style="font-size:1rem;">
  <p style="font-size:1em;">
    Rem and em are common CSS property values that are used for relative length. The CSS length value come in two different forms, absolute and relative. The absolute length is a fixed measurement that is specified by pixels. Relative lengths are a bit more complicated, they are not fixed units of measurement. This means the relative length depends on other factors, a use case would be creating a responsive web layout that depends on other length property. Rem and em are relative length that are used for their responsiveness and scalability. In this blog I will use rem and em for setting responsive and scalable font-size in this blog.
  </p>

  <p style="font-size:1em;">
    I was reading a blog post <b>Use rem for Global Sizing; Use em for Local Sizing</b> by Robin Rendle. You can read the blog <a href="https://css-tricks.com/rem-global-em-local/#more-239011" target="_blank">here</a>. I haven't used rem before and have seen it in some of the front-end frameworks like <a href="http://getbootstrap.com/" target="_blank">Bootstrap</a>, <a href="http://foundation.zurb.com/" target="_blank">Foundation</a>, and <a href="http://materializecss.com/" target="_blank">Materialize</a>. You can see that each of these front-end frameworks uses rem in their components by looking inside the sass folder in their github page. As I was reading this blog I learn more about em and rem. I wanted to understand more about rem and em by playing with them in this blog.
  </p>
</article>

<div class="font-size-control" style="margin:0 auto; text-align:center; border: 5px solid #00BCD4; padding: 10px;">
  Change the rem in the text above
  <p class="range-field">
    <input type="range" min="0.8" max="2.5" step="0.1" value="1">
  </p>
</div>

#### Conclusion

It's fun to play around with the rem and em unit length values to create responsive and scalable text. Using rem for global sizing and em for local sizing makes adjusting your stylesheet easier, all you have to do is change the root length of the html element.

> While em is relative to the font-size of its direct or nearest parent, rem is only relative to the html (root) font-size.

<script>
  (function($){
    $("input[type='range']").on("change", function() {
      console.log($(this).val());
      $(".module").css("font-size", $(this).val() + "rem");
    });
  })(jQuery);
</script>
