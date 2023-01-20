---
nav_title: "GET : Répertorier les ID de produit"
article_title: "GET : Répertorier les ID de produit"
search_tag: Endpoint
page_order: 1
layout: api_page
page_type: référence
description: "Cet article présente en détail l’endpoint Braze Répertorier les ID de produit."

---
{% api %}
# Endpoint Répertorier les ID de produit
{% apimethod get %}
/purchases/product_list
{% endapimethod %}

Utilisez cet endpoint pour renvoyer les listes paginées d’ID de produit.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#dff4ed40-81f5-451d-9d44-accc0e932285{% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='purchases product list' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `page` | Facultatif | String | La page de votre liste de produits que vous souhaitez afficher. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande

{% raw %}
```
https://rest.iad-01.braze.com/purchases/product_list?page=1
```
{% endraw %}

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "products": [
    "product_name" (string), le nom du produit
  ],
  "message": "réussite"
}
```

{% endapi %}
