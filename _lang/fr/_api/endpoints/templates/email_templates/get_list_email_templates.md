---
nav_title: "GET : Répertorier les modèles d’e-mail disponibles"
article_title: "GET : Répertorier les modèles d’e-mail disponibles"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Répertorier les modèles d’e-mail disponibles."

---
{% api %}
# Répertorier les modèles d’e-mail disponibles
{% apimethod get %}
/templates/email/list
{% endapimethod %}

Utilisez cet endpoint pour obtenir une liste des e-mails disponibles sur votre compte Braze.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#eec24bf4-a3f4-47cb-b4d8-bb8f03964cca {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `modified_after`  | Facultatif | Chaîne de caractères au format [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) | Récupérer uniquement les modèles mis à jour à l’heure donnée ou après. |
| `modified_before`  |  Facultatif | Chaîne de caractères au format [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) | Récupérer uniquement les modèles mis à jour à l’heure donnée ou avant. |
| `limit` | Facultatif | Nombre positif | Nombre maximum de modèles à récupérer. Par défaut à 100 si non renseigné, avec une valeur maximale acceptable de 1 000. |
| `offset`  |  Facultatif | Nombre positif | Nombre de modèles à ignorer avant de renvoyer le reste des modèles qui correspondent aux critères de recherche. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
```
curl --location --request GET 'https://rest.iad-01.braze.com/templates/email/list?modified_after=2020-01-01T01:01:01.000000&modified_before=2020-02-01T01:01:01.000000&limit=1&offset=0' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse 

{% alert important %}
Les modèles construits à l’aide de l’éditeur Drag & Drop ne sont pas fournis dans cette réponse.
{% endalert %}

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "count": le nombre de modèles renvoyés
  "templates": [modèle comportant les propriétés suivantes]:
    "email_template_id": (string) votre identifiant API du modèle d’e-mail,
    "template_name": (string) le nom de votre modèle d’e-mail,
    "created_at": (string) le moment auquel l’e-mail a été créé en ISO 8601,
    "updated_at": (string) le moment auquel l’e-mail a été mis à jour en ISO 8601,
    "tags": (array of strings) les balises jointes au modèle
}
```
{% endapi %}



