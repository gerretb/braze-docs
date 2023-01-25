---
nav_title: "GET : Liste des Canvas"
article_title: "GET : Liste des Canvas"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Liste de Canvas."

---
{% api %}
# Endpoint Liste de Canvas
{% apimethod get %}
/canvas/list
{% endapimethod %}

Utilisez cet endpoint pour exporter une liste de Canvas, y compris le nom, l’identifiant de l’API Canvas et les balises associées. Les Canvas sont renvoyés par groupes de 100 triés par date de création (des plus anciens au plus récents par défaut).

Les Canvas archivés ne seront pas inclus dans la réponse API, sauf si le champ `include_archived` est spécifié. En revanche, les Canvas arrêtés mais non archivés seront renvoyés par défaut.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#e6c150d7-fceb-4b10-91e2-a9ca4d5806d1 {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | -------- | --------- | ----------- |
| `page` | Facultatif | Integer   | La page des Canvas à renvoyer, par défaut sur `0` (renvoie le premier ensemble jusqu’à 100 éléments) |
| `include_archived` | Facultatif | Boolean | S'il faut inclure ou non des Canvas archivés, par défaut sur `false`. |
| `sort_direction` | Facultatif | String | - Trier l'heure de création de la plus récente à la plus ancienne : indiquer la valeur `desc`.<br> - Trier l'heure de création de la plus ancienne à la plus récente : indiquer la valeur `asc`. <br><br>Si `sort_direction` n’est pas inclus, l’ordre par défaut est du plus ancien au plus récent. |
| `last_edit.time[gt]` | Facultatif | Date | Filtre les résultats et renvoie uniquement les Canvas qui ont été modifiés au-delà de l’heure indiquée jusqu’à maintenant. Le format est `yyyy-MM-DDTHH:mm:ss`. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location -g --request GET 'https://rest.iad-01.braze.com/canvas/list?page=1&include_archived=false&sort_direction=desc&last_edit.time[gt]=2020-06-28T23:59:59-5:00' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "canvases" : [
  	{
  		"id" : (string) l’identifiant API Canvas,
  		"last_edited": (ISO 8601 string) la dernière date d’édition du message,
  		"name" : (string) le nom du Canvas,
  		"tags" : (array) les noms de balise associés au Canvas formatés en tant que chaînes de caractères,
  	},
    ... (plus de Canvas)
  ],
  "message": (required, string) le statut de l’exportation, renvoie « réussite » lorsqu’elle s’achève sans erreur
}
```

{% alert tip %}
Pour obtenir de l'aide sur les exportations CSV et de l'API, consultez la section [Résolution des problèmes d'exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
