---
nav_title: "GET : Analyse des segments"
article_title: "GET : Analyse des segments"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: référence
description: "Cet article présente en détail l’endpoint Obtenir les analyses de segment et son utilisation."

---
{% api %}
# Endpoint Analyse des segments
{% apimethod get %}
/segments/data_series
{% endapimethod %}

Utilisez cet endpoint pour récupérer une série quotidienne de la taille estimée d’un segment au fil du temps.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#62d9d142-cdec-4aea-a287-c13efea7415e {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | -------- | --------- | ----------- |
| `segment_id` | Requis | String | Voir [Identifiant API de segment]({{site.baseurl}}/api/identifier_types/).<br><br> Le `segment_id` pour un segment donné se trouve dans votre **Console du développeur** sur votre compte Braze, sinon vous pouvez utiliser l'[endpoint Liste des segments]({{site.baseurl}}/api/endpoints/export/segments/get_segment/).  |
| `length` | Requis | Integer | Nombre maximum de jours avant `ending_at` à inclure dans la série renvoyée. Doit être compris entre 1 et 100 (inclus). |
| `ending_at` | Facultatif | DateTime <br>(chaîne de caractères [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601)) | Date à laquelle la série de données doit se terminer. Par défaut, l’heure de la demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
{% raw %}
```
curl --location -g --request GET 'https://rest.iad-01.braze.com/segments/data_series?segment_id={{segment_identifier}}&length=14&ending_at=2018-06-27T23:59:59-5:00' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```
{% endraw %}

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) le statut de l’exportation, renvoie « réussite » lorsqu’elle s’achève sans erreur,
    "data" : [
        {
            "time" : (string) la date en tant que date ISO 8601,
            "size" : (int) la taille du segment à cette date
        },
        ...
    ]
}
```

{% alert tip %}
Pour obtenir de l'aide sur les exportations CSV et de l'API, consultez la section [Résolution des problèmes d'exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
