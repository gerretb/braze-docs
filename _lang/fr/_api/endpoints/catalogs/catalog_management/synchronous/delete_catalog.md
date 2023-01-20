---
nav_title: "SUPPRIMER : Supprimer un catalogue"
article_title: "SUPPRIMER : Supprimer un catalogue"
search_tag: Endpoint
page_order: 1

layout: api_page
page_type: référence
description: "Cet article présente en détail l’endpoint de Braze Supprimer un catalogue."

---
{% api %}
# Supprimer un catalogue
{% apimethod delete %}
/catalogs/{catalog_name}
{% endapimethod %}

Utilisez cet endpoint pour supprimer un catalogue.

## Limites de débit

Cet endpoint a une limitation du débit partagée de 5 requêtes par minute entre tous les endpoints synchronisés du catalogue.

## Paramètres de chemin

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `catalog_name` | Requis | String | Nom du catalogue. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Paramètres de demande

Cet endpoint n’a pas de corps de demande.

## Exemple de demande

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
```

## Réponse

Deux réponses de code d’état existent pour cet endpoint : `200` et `404`..

### Exemple de réponse réussie

Le code de statut `200` pourrait retourner le corps de réponse suivant.

```json
{
  "message": "réussite"
}
```

### Exemple de réponse échouée

Le code de statut `404` pourrait retourner le corps de réponse suivant. Consultez la [résolution des problèmes](#troubleshooting) pour plus d’informations concernant les erreurs que vous pourriez rencontrer.

```json
{
  "errors": [
    {
      "id": "catalog-not-found",
      "message": "Catalogue introuvable",
      "parameters": [
        "catalog_name"
      ],
      "parameter_values": [
        "restaurants"
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
| `catalog-not-found` | Vérifiez que le nom du catalogue est valide. |
{: .reset-td-br-1 .reset-td-br-2}

{% endapi %}