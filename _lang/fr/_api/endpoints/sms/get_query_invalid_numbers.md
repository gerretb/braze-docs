---
nav_title: "GET : Requête des numéros de téléphone non valides"
article_title: "GET : Requête des numéros de téléphone non valides"
search_tag: Endpoint
page_order: 1
layout: api_page
page_type: reference
description: "Cet article décrit l’utilisation et les paramètres pour se servir de l’endpoint Braze Récupérer une liste des numéros de téléphone non valides."
---
{% api %}
# Requête ou liste des numéros de téléphone non valides
{% apimethod get %}
/sms/invalid_phone_numbers
{% endapimethod %}

Cet endpoint vous permet d’extraire une liste des numéros de téléphone considérés comme « non valides » dans un certain laps de temps.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#81ceae19-15d1-4ac1-ad22-a6b86a92456d {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| ----------|-----------| ----------|----- |
| `start_date` | Facultatif <br>(voir la note) | Chaîne de caractères au format AAAA-MM-JJ| La date de début de la plage pour récupérer les numéros de téléphone non valides doit être antérieure à `end_date`. Ce traitement est effectué à minuit (UTC) par l’API. |
| `end_date` | Facultatif <br>(voir la note) | Chaîne de caractères au format AAAA-MM-JJ | Date de fin de la plage pour récupérer les numéros de téléphone non valides. Ce traitement est effectué à minuit (UTC) par l’API. |
| `limit` | Facultatif | Integer | Champ facultatif pour limiter le nombre de résultats renvoyés. Par défaut à 100, le maximum est 500. |
| `offset` | Facultatif | Integer | Point de départ facultatif dans la liste où récupérer les informations. |
| `phone_numbers` | Facultatif <br>(voir la note) | Tableau de chaînes de caractères au format e.164 | S’il est fourni, nous renverrons le numéro de téléphone s’il s’avère non valide. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

{% alert note %}
Vous devez fournir une `start_date` et une `end_date`, OU un `phone_numbers`. Si vous fournissez les trois, une `start_date`, une `end_date`, et un `phone_numbers`, nous donnerons la priorité aux numéros de téléphone communiqués et ignorerons la plage de dates.
{% endalert %}

Si votre plage de dates dépasse le nombre `limit` de numéros de téléphone non valides, vous devrez effectuer plusieurs appels d’API, en augmentant à chaque fois le `offset` jusqu’à ce qu’un appel renvoie un résultat inférieur à `limit` ou égal à zéro.

## Exemple de demande
```
curl --location --request GET 'https://rest.iad-01.braze.com/sms/invalid_phone_numbers?start_date=2019-01-01&end_date=2019-02-01&limit=100&offset=1&phone_numbers[]=12345678901' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE'
```

## Réponse
Les entrées sont répertoriées par ordre décroissant.

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "sms": [
    {
      "phone": (string) le numéro de téléphone au format E.164,
      "invalid_detected_at": (string) l’heure à laquelle le numéro invalide a été détecté dans le format ISO 8601
    },
    {
      "phone": (string) le numéro de téléphone au format E.164,
      "invalid_detected_at": (string) l’heure à laquelle le numéro invalide a été détecté dans le format ISO 8601
    },
    {
      "phone": (string) le numéro de téléphone au format E.164,
      "invalid_detected_at": (string) l’heure à laquelle le numéro invalide a été détecté dans le format ISO 8601
    }
  ],
  "message": "success"
}
```
{% endapi %}