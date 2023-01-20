---
nav_title: "Alias pour identifier un objet"
article_title: Alias API pour identifier un objet
page_order: 11
page_type: référence
description: "Cet article explique l’objet nécessaire pour identifier les alias utilisateurs."

---

# Spécification des alias pour identifier un objet

Une demande API contenant l’un des champs de l’objet Attributs créera ou mettra à jour un attribut de ce nom avec la valeur donnée sur le profil utilisateur spécifié. Utilisez les champs de profil utilisateur de Braze (énumérés comme suit ou ceux énumérés dans la section des [champs de profils utilisateur de Braze]({{site.baseurl}}/api/objects_filters/user_attributes_object/#braze-user-profile-fields)) pour mettre à jour ces valeurs spéciales sur le profil utilisateur dans le tableau de bord ou ajouter vos propres données d’attributs personnalisés à l’utilisateur.

## Corps de l’objet

```json
{
  "aliases_to_identify" : (required, array of Aliases to Identify Object)
  [
    {
      "external_id" : (required, string) voir ID utilisateur externe,
      // external_ids pour les utilisateurs qui n’existent pas retournera une erreur non fatale.
      // Voir les réponses du serveur pour obtenir des détails.
      "user_alias" : {
        "alias_name" : (required, string) voir Alias d’utilisateur,
        "alias_label" : (required, string) voir Alias d’utilisateur
      }
    }
  ]
}
```

- [ID utilisateur externe]({{site.baseurl}}/api/objects_filters/user_attributes_object/#braze-user-profile-fields)
- [Alias utilisateur]({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_profile_lifecycle/#user-aliases)
