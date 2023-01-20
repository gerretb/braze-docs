---
nav_title: "GET : Requête de la liste des adresses e-mail désinscrites"
article_title: "GET : Requête de la liste des adresses e-mail désinscrites"
search_tag: Endpoint
page_order: 1
layout: api_page
page_type: référence
description: "Cet article décrit l’utilisation et les paramètres pour se servir de l’endpoint Braze Obtenir les désinscriptions aux e-mails."

---
{% api %}
# Récupérer la liste ou demander les désinscriptions aux e-mails
{% apimethod get %}
/email/unsubscribes
{% endapimethod %}

Utilisez cet endpoint pour renvoyer les e-mails qui ont été désinscrits entre le `start_date` et le `end_date`. Vous pouvez utiliser cet endpoint pour configurer une synchronisation bidirectionnelle entre Braze et d’autres systèmes de messagerie ou votre propre base de données.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#d2966b81-188a-407b-ba7e-e6c252c44b4a {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| ----------|-----------| ---------|------ |
| `start_date` | Facultatif <br>(voir la note) | Chaîne de caractères au format AAAA-MM-JJ| La date de début de la plage pour récupérer les désinscriptions doit être antérieure à end_date. Ce traitement est effectué à minuit (UTC) par l’API. |
| `end_date` | Facultatif <br>(voir la note) | Chaîne de caractères au format AAAA-MM-JJ | La date de fin de la plage pour récupérer les désinscriptions. Ce traitement est effectué à minuit (UTC) par l’API. |
| `limit` | Facultatif | Integer | Champ facultatif pour limiter le nombre de résultats renvoyés. Par défaut à 100, le maximum est 500. |
| `offset` | Facultatif | Integer | Point de départ facultatif dans la liste où récupérer les informations. |
| `sort_direction` | Facultatif | String | Indiquez la valeur `asc` pour trier les désinscriptions de la plus ancienne à la plus récente. Indiquez la valeur `desc` pour trier de la plus récente à la plus ancienne. Si `sort_direction` n’est pas inclus, l’ordre par défaut est du plus récent au plus ancien. |
| `email` | Facultatif <br>(voir la note) | String | S’il est fourni, nous renverrons si l’utilisateur s’est désinscrit ou pas. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

{% alert note %}
Vous devez fournir un `end_date`, ainsi qu’un `email` ou un `start_date`..
{% endalert %}

Si votre plage de dates dépasse le nombre `limit` de désinscriptions, vous devrez effectuer plusieurs appels d’API, en augmentant à chaque fois le `offset` jusqu’à ce qu’un appel renvoie un résultat inférieur à `limit` ou égal à zéro.

## Exemple de demande 
```
curl --location --request GET 'https://rest.iad-01.braze.com/email/unsubscribes?start_date=2020-01-01&end_date=2020-02-01&limit=1&offset=1&sort_direction=desc&email=example@braze.com' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE'
```

## Réponse

Les entrées sont répertoriées par ordre décroissant.

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "emails": [
    {
      "email": (string) un e-mail qui vient d’être désinscrit,
      "unsubscribed_at": (string) le moment auquel l’e-mail a été désinscrit en ISO 8601
    },
    {
      "email": (string) un e-mail qui vient d’être désinscrit,
      "unsubscribed_at": (string) le moment auquel l’e-mail a été désinscrit en ISO 8601
    },
    {
      "email": (string) un e-mail qui vient d’être désinscrit,
      "unsubscribed_at": (string) le moment auquel l’e-mail a été désinscrit en ISO 8601
    }
  ],
  "message": "réussite"
}
```
{% endapi %}
