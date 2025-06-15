# Shopfiy
#Star
Dynamic New Section in Shopify
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />
<style>
.star-filled {
    color: gold;
}
  .star-empty {
    color: lightgray;
  }
  </style>
<div class="first_star">
  <h3>{{ section.settings.star_text }}</h3>
</div>

<div class="real_star">
  
  {% if section.settings.star_range %}
    {% for i in (1..section.settings.star_range) %}
     <i class="fa-solid fa-star" {% if i <= star_range %}star-filled{% else %}star-empty{% endif %}></i>

    {% endfor %}
  {% endif %}
</div>

{% schema %}
{
"name": "Section name",
  "settings": [
    {
      "type": "richtext",
      "id": "star_text",
      "label": "Heading"
    },
    {
      "type": "range",
      "id": "star_range",
      "label": "Star rating",
      "min": 1,
      "max": 5,
      "step": 1,
      "default": 3,
      "unit": "rtg"
    }
  ],
  "presets": [
    {
      "name": "star"
    }
  ]
}
{% endschema %}
#New Collection 
{% assign collectionon = section.settings.collectionone %}
{% assign varitant_collection = collections[collectionon] %}
{% for product in varitant_collection.products %}
{{ product.featured_image  | image_url:"master" | img_tag }}
   {{ product.price | money }}
  {% endfor %}
  {% schema %}
    {
      "name":"Colletion",
      "settings": [
        {
          "type":"collection",
          "id": "collectionone",
          "label": "Collection SKL"
        }
      ],
      "presets": [
        {
        "name": "Collection SKl"
        }
          ]
    }
  {% endschema %}
  #New Figma
  <!-- Header -->
<header class="site-header" style="display: flex; justify-content: space-between; align-items: center; padding: 20px; background: #f5f5f5;">
  <div class="logo"><h1>SareeShop</h1></div>
  <nav class="nav-links" style="display: flex; gap: 20px;">
    <a href="/">Home</a>
    <a href="/collections/all">Shop</a>
    <a href="/pages/about">About</a>
    <a href="/pages/contact">Contact</a>
  </nav>
  <div class="cart-icon">
    <a href="/cart">🛒</a>
  </div>
</header>

<!-- Hero Banner -->
<section class="hero" style="text-align: center; background: url('{{ 'banner.jpg' | asset_url }}') no-repeat center center/cover; height: 400px; display: flex; align-items: center; justify-content: center;">
  <div>
    <h2 style="color: white; font-size: 36px;">Elegance in Every Drape</h2>
    <a href="/collections/all" style="background: black; color: white; padding: 10px 20px; text-decoration: none;">Shop Now</a>
  </div>
</section>

<!-- Featured Collections -->
<section class="featured-collections" style="padding: 40px; text-align: center;">
  <h2>Featured Collections</h2>
  <div style="display: flex; justify-content: center; gap: 20px; margin-top: 20px;">
    {% for collection in collections limit:3 %}
      <div>
        <a href="{{ collection.url }}">
          <img src="{{ collection.image | img_url: 'medium' }}" alt="{{ collection.title }}" style="width: 200px; height: 200px; object-fit: cover;">
          <h3>{{ collection.title }}</h3>
        </a>
      </div>
    {% endfor %}
  </div>
</section>

<!-- Product Grid -->
<section class="product-grid" style="padding: 40px;">
  <h2 style="text-align: center;">Our Products</h2>
  <div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; margin-top: 20px;">
    {% for product in collections.all.products limit:4 %}
      <div style="border: 1px solid #ccc; padding: 10px; width: 220px;">
        <a href="{{ product.url }}">
          <img src="{{ product.featured_image | img_url: 'medium' }}" alt="{{ product.title }}" style="width: 100%; height: 200px; object-fit: cover;">
          <h3>{{ product.title }}</h3>
        </a>
        <p>{{ product.price | money }}</p>
        <form method="post" action="/cart/add">
          <input type="hidden" name="id" value="{{ product.variants.first.id }}">
          <button type="submit" style="padding: 8px 12px; background: black; color: white; border: none; cursor: pointer;">Add to Cart</button>
        </form>
      </div>
    {% endfor %}
  </div>
</section>

<!-- Footer -->
<footer class="site-footer" style="background: #f5f5f5; padding: 30px; text-align: center;">
  <p>&copy; 2025 SareeShop. All rights reserved.</p>
  <p>
    <a href="#">Instagram</a> |
    <a href="#">Facebook</a> |
    <a href="#">Twitter</a>
  </p>
</footer>
{% schema %}
{
  "name": "Custom Home Page",
  "tag": "section",
  "class": "custom-home-section",
  "settings": [
    {
      "type": "text",
      "id": "hero_heading",
      "label": "Hero Heading",
      "default": "Elegance in Every Drape"
    },
    {
      "type": "image_picker",
      "id": "hero_image",
      "label": "Hero Image"
    },
    {
      "type": "url",
      "id": "hero_button_link",
      "label": "Hero Button Link",
      "default": "/collections/all"
    },
    {
      "type": "text",
      "id": "hero_button_text",
      "label": "Hero Button Text",
      "default": "Shop Now"
    }
  ],
  "presets": [
    {
      "name": "Custom Homepage Section",
      "category": "Homepage"
    }
  ]
}
{% endschema %}
#Snippet 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>5 Same Size Images</title>
  <style>
    .image-container {
      display: flex;
      gap: 20px;
      justify-content: center;
      align-items: center;
      padding: 30px;
      background-color: #f9f9f9;
      flex-wrap: wrap;
    }

    .image-container img {
      width: 200px;
      height: 200px;
      object-fit: cover;
      border-radius: 50%;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }

    .image-container img:not(:first-child)
 {
    margin-left: -5%;
}
  </style>
</head>
<body>

  <div class="image-container">
   <img src="{{ section.settings.frist_img | image_url: 'master' }}">
<img src="{{ section.settings.sec_img | image_url: 'master' }}">
<img src="{{ section.settings.third_img | image_url: 'master' }}">
<img src="{{ section.settings.fourth_img | image_url: 'master' }}">
<img src="{{ section.settings.five_img | image_url: 'master' }}">

    <div class="second">
<p>{{ emogi_text }}</p>
<span>{{ emogi_text_sec }}</span>  
</div>
</div>
</body>
</html>
