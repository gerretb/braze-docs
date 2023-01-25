---
nav_title: "GET : Liste des événements personnalisés"
article_title: "GET : Liste des événements personnalisés"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Liste des événements personnalisés."

---
{% api %}
# Obtenir la liste des événements personnalisés
{% apimethod get %}
/events/list
{% endapimethod %}

Utilisez cet endpoint pour exporter une liste d’événements personnalisés qui ont été enregistrés pour votre application. Les noms des événements sont renvoyés par groupes de 250, triés par ordre alphabétique.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#93ecd8a5-305d-4b72-ae33-2d74983255c1 {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='events list' %}

## Paramètres de demande

| Paramètre| Requis | Type de données | Description |
| -------- | -------- | --------- | ----------- |
| `page` | Facultatif | Integer | La page des noms d’événement à renvoyer, par défaut sur 0 (renvoie le premier ensemble jusqu’à 250 éléments). |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request GET 'https://rest.iad-01.braze.com/events/list?page=3' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) le statut de l’exportation, renvoie « réussite » lorsqu’elle s’achève sans erreur,
    "events" : [
        "Event A", (string) the event name,
        "Event B", (string) the event name,
        "Event C", (string) the event name,
        ...
    ]
}
```

### Codes de réponse des erreurs fatales {#fatal-export}

Les codes d’état suivants et les messages d’erreur associés seront renvoyés si votre demande rencontre une erreur fatale. L’un de ces codes d’erreur indique qu’aucune donnée ne sera traitée.

| Code d’erreur       | Raison/Cause                                                   |
| ---------------- | ---------------------------------------------------------------- |
| 400 Demande erronée  | Syntaxe incorrecte                                                       |
| 401 Non autorisé | Clé API REST inconnue ou manquante                                  |
| 429 Débit limité | Limite de débit dépassée                                                  |
| 5XX              | Erreur de serveur interne, vous devriez réessayer avec le délai exponentiel |
{: .reset-td-br-1 .reset-td-br-2}

{% alert tip %}
Pour obtenir de l'aide sur les exportations CSV et de l'API, consultez la section [Résolution des problèmes d'exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
