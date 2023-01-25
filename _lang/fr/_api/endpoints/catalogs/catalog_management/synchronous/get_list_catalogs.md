---
nav_title: "GET : Lister des catalogues"
article_title: "GET : Lister des catalogues"
search_tag: Endpoint
page_order: 2

layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint de Braze Lister les catalogue."

---
{% api %}
# Lister les catalogues dans le groupe d'apps
{% apimethod get %}
/catalogs
{% endapimethod %}

Utilisez cet endpoint pour renvoyer une liste de catalogues dans le groupe d’apps.

## Limites de débit

Cet endpoint a une limitation du débit partagée de 5 requêtes par minute entre tous les endpoints synchronisés du catalogue.

## Paramètres de chemin

Cet endpoint n’a pas de chemin de paramètres.

## Paramètres de demande

Cet endpoint n’a pas de corps de demande.

### Exemple de demande

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

### Exemple de réponse réussie

Le code de statut `200` pourrait retourner le corps de réponse suivant.

```json
{
  "catalogs": [
    {
      "description": "Mes restaurants",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "Nom",
          "type": "string"
        },
        {
          "name": "Ville",
          "type": "string"
        },
        {
          "name": "Cuisine",
          "type": "string"
        },
        {
          "name": "Note",
          "type": "number"
        },
        {
          "name": "Loyalty_Program",
          "type": "boolean"
        },
        {
          "name": "Created_At",
          "type": "time"
        }
      ],
      "name": "restaurants",
      "num_items": 10,
      "updated_at": "2022-11-02T20:04:06.879+00:00"
    },
    {
      "description": "Mon catalogue",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "string_field",
          "type": "string"
        },
        {
          "name": "number_field",
          "type": "number"
        },
        {
          "name": "boolean_field",
          "type": "boolean"
        },
        {
          "name": "time_field",
          "type": "time"
        },
      ],
      "name": "my_catalog",
      "num_items": 3,
      "updated_at": "2022-11-02T09:03:19.967+00:00"
    },
  ],
  "message": "success"
}
```

{% endapi %}