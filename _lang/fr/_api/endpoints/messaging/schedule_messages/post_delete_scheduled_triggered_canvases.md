---
nav_title: "POST : Supprimer des Canvas planifiés déclenchés par API"
article_title: "POST : Supprimer des Canvas planifiés déclenchés par API"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: référence
description: "Cet article présente en détail l’endpoint Braze Supprimer les Canvas déclenchés par API et planifiés."

---
{% api %}
# Supprimer des Canvas planifiés déclenchés par API
{% apimethod post core_endpoint|https://www.braze.com/docs/core_endpoints %} 
/canvas/trigger/schedule/delete
{% endapimethod %}

L’endpoint de suppression de la planification vous permet d’annuler un message que vous avez déjà planifié dans des Canvas déclenchés par API avant qu’il ne soit envoyé.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#7d34037f-4bf2-4fab-bc9c-c972988051a7 {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Corps de la demande

Les messages ou déclencheurs planifiés qui sont supprimés peu de temps avant ou pendant l’heure où ils sont censés être envoyés seront mis à jour dans les meilleurs délais, de sorte que les suppressions de dernière minute pourraient être appliquées à tous, certains ou aucun de vos utilisateurs ciblés.

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "canvas_id": (required, string) l’identifiant Canvas,
  "schedule_id": (required, string) Le `schedule_id` à supprimer (obtenu à partir de la réponse pour créer une planification).
}
```

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | ---------| --------- | ----------- |
| `canvas_id`| Requis | String | Voir [Identifiant Canvas]({{site.baseurl}}/api/identifier_types/). |
| `schedule_id` | Requis | String | Le `schedule_id` à supprimer (obtenu à partir de la réponse pour créer une planification). |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}


## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/canvas/trigger/schedule/delete' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "canvas_id": "canvas_identifier",
  "schedule_id": "schedule_identifier"
}'
```

{% endapi %}
