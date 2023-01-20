---
nav_title: "GET : Liste des cartes de fil d’actualité"
article_title: "GET : Liste des cartes de fil d’actualité"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: référence
description: "Cet article présente en détail l’endpoint Liste de la carte de fil d’actualité."

---
{% api %}
# Endpoint Liste des cartes de fil d’actualité
{% apimethod get %}
/feed/list
{% endapimethod %}

Utilisez cet endpoint pour exporter une liste de cartes de fil d’actualité, chacune incluant son nom et son identifiant API de carte. Les cartes sont renvoyées par groupes de 100 triés par date de création (des plus anciens au plus récents par défaut).

{% alert note %}
Les fils d'actualités deviennent obsolètes. Braze recommande aux clients qui utilisent son outil Fil d'actualité de passer à son canal de communication de cartes de contenu qui est plus flexible, personnalisable et fiable. Pour en savoir plus, consultez le [guide de migration]({{site.baseurl}}/user_guide/message_building_by_channel/content_cards/migrating_from_news_feed/).
{% endalert %}

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#9fa7a3bc-4a02-4de2-bc4c-8f111750665e {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | -------- | --------- | ----------- |
| `page` | Facultatif | Integer   | La page des cartes à renvoyer, par défaut sur 0 (renvoie le premier ensemble jusqu’à 100 éléments). |
| `include_archived` | Facultatif | Boolean   | S’il faut inclure ou non des cartes archivées, par défaut sur Faux. |
| `sort_direction` | Facultatif | String | Trier l'heure de création de la plus récente à la plus ancienne : indiquer la valeur `desc`.<br> - Trier l'heure de création de la plus ancienne à la plus récente : indiquer la valeur `asc`. <br><br>Si `sort_direction` n’est pas inclus, l’ordre par défaut est du plus ancien au plus récent. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request GET 'https://rest.iad-01.braze.com/feed/list?page=1&include_archived=true&sort_direction=desc' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) le statut de l’exportation, renvoie « réussite » lorsqu’elle s’achève sans erreur,
    "cards" : [
        {
            "id" : (string) l’identifiant API de carte,
            "type" : (string) type de carte : NewsItem (cartes habituelles), CaptionedImage, Banner
            "title" : (string) le titre de la carte,
            "tags" : (array) les noms de balise associés à la carte
        },
        ...
    ]
}
```

{% alert tip %}
Pour obtenir de l'aide sur les exportations CSV et de l'API, consultez la section [Résolution des problèmes d'exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
