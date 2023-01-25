---
nav_title: "GET : Lister les détails de plusieurs produits du catalogue"
article_title: "GET : Lister les détails de plusieurs produits du catalogue"
search_tag: Endpoint
page_order: 3

layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint de Braze Lister les détails de plusieurs produits du catalogue."

---
{% api %}
# Lister les détails de plusieurs produits du catalogue
{% apimethod get %}
/catalogs/{catalog_name}/items
{% endapimethod %}

Utilisez cet endpoint pour retourner plusieurs produits du catalogue et leur contenu.

## Limites de débit

Cet endpoint a une limitation du débit partagée de 50 requêtes par minute entre tous les endpoints synchronisés de produits du catalogue.

## Paramètres de chemin

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Requis | String | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de recherche

Notez que chaque appel de cet endpoint retournera 50 produits. Pour un catalogue ayant plus de 50 produits, utilisez l’en-tête `Link` pour extraire les données de la page suivante tel que montré dans l’exemple de réponse suivant.

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `cursor` | Facultatif | String | Détermine la pagination des produits du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de demande

Cet endpoint n’a pas de corps de demande.

## Exemple de requêtes

### Sans curseur

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

### Avec curseur

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items?cursor=c2tpcDow' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```

## Réponse

Trois réponses de code d’état existent pour cet endpoint : `200`, `400` et `404`..

### Exemple de réponse réussie

Le code de statut `200` pourrait retourner l’en-tête et le corps de réponse suivant.

{% alert note %}
L’en-tête `Link` n’existera pas si le catalogue possède 50 produits ou moins. Pour les appels sans curseur, `prev` ne s’affichera pas. Lors de la consultation de la dernière page de produits, `next` ne s’affichera pas.
{% endalert %}

```
Link: </catalogs/all_restaurants/items?cursor=c2tpcDow>; rel="prev",</catalogs/all_restaurants/items?cursor=c2tpcDoxMDA=>; rel="next"
```

```json
{
  "items": [
    {
      "id": "restaurant1",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "Américain",
      "Rating": 5,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    },
    {
      "id": "restaurant2",
      "Name": "Restaurant2",
      "City": "New York",
      "Cuisine": "Américain",
      "Rating": 10,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    },
    {
      "id": "restaurant3",
      "Name": "Restaurant3",
      "City": "New York",
      "Cuisine": "Américain",
      "Rating": 5,
      "Loyalty_Program": false,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    }
  ],
  "message": "success"
}
```

### Exemple de réponse échouée

Le code de statut `400` pourrait retourner le corps de réponse suivant. Consultez la [résolution des problèmes](#troubleshooting) pour plus d’informations concernant les erreurs que vous pourriez rencontrer.

```json
{
  "errors": [
    {
      "id": "invalid-cursor",
      "message": "« cursor » (curseur) n’est pas valide",
      "parameters": [
        "cursor"
      ],
      "parameter_values": [
        "bad-cursor"
      ]
    }
  ],
  "message": "Requête invalide"
}
```

## Résolution des problèmes

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de résolution des problèmes associées.

| Erreur | Résolution des problèmes |
| --- | --- |
| `invalid-cursor` | Vérifiez que votre `cursor` est valide. |
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}