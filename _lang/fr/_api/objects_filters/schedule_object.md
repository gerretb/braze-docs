---
nav_title: "Objet de planification"
article_title: Objet de planification API
page_order: 12
page_type: reference
description: "Cet article répertorie et explique l’objet de planification différent utilisé chez Braze."

---

# Spécification de l’objet de planification

Les paramètres des endpoints de création de planification de campagne et de Canvas reflètent ceux de l’endpoint d’envoi et ajoutent le paramètre `schedule` qui vous permet de spécifier si vous souhaitez que vos utilisateurs ciblés reçoivent votre message (jusque dans les 90 jours suivants). Si vous incluez uniquement le paramètre `time` dans l’objet `schedule`, tous vos utilisateurs recevront des messages à ce moment-là.

Si vous avez défini `in_local_time` sur `true`, vos utilisateurs recevront le message à la date et l’heure désignées dans leurs fuseaux horaires respectifs. Si `in_local_time` est vrai, vous obtiendrez une réponse d’erreur si le paramètre `time` est passé dans le fuseau horaire de votre entreprise. Si vous avez défini `at_optimal_time` sur vrai, vos utilisateurs recevront le message à la date indiquée et à l’[heure optimale][33] pour eux (indépendamment de l’heure que vous fournissez). Lors de l’utilisation d’un envoi à l’heure local ou optimale, ne fournissez pas de désignateurs de fuseau horaire dans la valeur du paramètre de temps (par ex., il suffit de nous indiquer `"2015-02-20T13:14:47"` plutôt que `"2015-02-20T13:14:47-05:00"`).

La réponse vous fournira un `schedule_id` que vous devez enregistrer au cas où vous auriez ultérieurement besoin d’annuler ou de mettre à jour le message que vous planifiez :

## Corps de l’objet

Insérez cet objet si nécessaire pour planifier vos messages.

```json
"schedule": {
  "time": (required, datetime as ISO 8601 string) moment d’envoi du message (jusqu’à 90 jours dans le futur),
  "in_local_time": (optional, bool),
  "at_optimal_time": (optional, bool),
}
```

## Réponse de l’ID de planification

Vous recevrez un `schedule_id` pour le message planifié que vous avez créé.

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "schedule_id" : (required, string) identifiant du message de planification qui a été créé
}
```

Les clients utilisant l’API pour les appels de serveur à serveur peuvent avoir besoin d’ajouter à leur liste blanche l’URL d’API appropriée s’ils se trouvent derrière un pare-feu.

Les réponses des endpoints de planification des messages incluront le `dispatch_id` du message pour y faire référence lors de l’envoi. Le `dispatch_id` est l’ID de distribution du message (ID unique pour chaque « transmission » envoyée depuis la plateforme Braze).

[33]: {{site.baseurl}}/user_guide/intelligence/intelligent_timing/
