---
nav_title: Google Tag Manager
article_title: Google Tag Manager pour le Web
platform: Web
page_order: 20
description: "Cet article explique comment utiliser Google Tag Manager pour déployer Braze sur votre site Internet."

---

# Google Tag Manager

> Cet article fournit un guide étape par étape sur la façon d’ajouter le SDK Braze pour le Web à votre site Internet à l’aide de Google Tag Manager. [Google Tag Manager][2] vous permet d’ajouter, de supprimer et de modifier à distance des balises sur votre site Internet sans avoir besoin d’une version de code de production ou de ressources d’ingénierie.

Braze a construit deux modèles Google Tag Manager : la [balise d’initialisation](#initialization-tag) et la [balise d’actions](#actions-tag).

Ces deux balises peuvent être ajoutées à votre espace de travail depuis la [galerie communautaire de Google ][15] ou en recherchant Braze lors de l’ajout d’une nouvelle balise à partir des modèles de la communauté.

![image de la galerie de recherche][gtm-community-gallery-search]

## Modèle de balise d’initialisation {#initialization-tag}

Utilisez la balise d’initialisation pour ajouter le SDK Braze pour le Web à votre site Internet.

### Étape 1 : Sélectionner la balise d’initialisation

Recherchez Braze dans la galerie de modèles de la communauté, puis sélectionnez la **balise d’initialisation de Braze**.

![Une boîte de dialogue affichant les paramètres de configuration de la balise d’initialisation de Braze. Les paramètres inclus sont les suivants : « type de balise », « clé API », « endpoint de l’API », « version du SDK », « ID d’utilisateur externe » et « ID de notification push pour le Web de Safari ».][gtm-initialization-tag]

### Étape 2 : Configurer les paramètres

Saisissez votre clé d’identification de l’API Braze et l’endpoint du SDK, que vous trouverez dans la page **Gérer les paramètres** du tableau de bord.

### Étape 3 : Choisir les options d’initialisation

Choisissez parmi l’ensemble d’options d’initialisation supplémentaires et facultatives décrites dans le guide de [configuration initiale][7].

### Étape 4 : Vérifier et réaliser la QA

Une fois que vous avez déployé cette balise, il existe deux manières de vérifier que l’intégration est correcte :

1. À l’aide de [l’outil de débogage][gtm-debugging-tool] de Google Tag Manager, vous devriez voir que la balise d’initialisation de Braze a été déclenchée sur vos pages ou vos événements configurés.
2. Vous devriez voir les demandes réseau faites à Braze et la bibliothèque globale `window.braze` devrait maintenant être définie sur votre page Web.

## Modèle de balises d’actions {#actions-tag}

Le modèle de balises d’actions de Braze vous permet de déclencher des événements personnalisés, de suivre les achats, de modifier les ID utilisateur et d’arrêter ou de reprendre le traçage selon les exigences de confidentialité.

![][gtm-actions-tag]

### Modifier l’ID externe de l’utilisateur {#external-id}

Le type de balise **Modifier l’utilisateur** appelle la [`changeUser`méthode](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#changeuser). 

Utilisez cette balise chaque fois qu’un utilisateur se connecte ou est identifié de quelque manière que ce soit par son identifiant unique `external_id`.

Veillez à saisir l’ID unique de l’utilisateur actuel dans le champ **ID externe de l’utilisateur**, généralement rempli à l’aide d’une variable de couche de données envoyée par votre site Internet.

![Une boîte de dialogue affichant les paramètres de configuration de la balise d’action de Braze. Les paramètres inclus sont « type de balise » et « ID externe de l’utilisateur »][gtm-change-user]

### Enregistrer les événements personnalisés {#custom-events}

Le type de balise **Événement personnalisé** appelle la [`logCustomEvent`méthode](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#logcustomevent).

Utilisez cette balise pour envoyer des événements personnalisés à Braze. Vous pouvez y inclure, de manière factultative, des propriétés de l’événement personnalisées.

Saisissez le **Nom de l’événement** en utilisant une variable ou en tapant un nom d’événement.

Utilisez le bouton **Ajouter une ligne** pour ajouter les propriétés de l’événement.

![Une boîte de dialogue affichant les paramètres de configuration de la balise d’action de Braze. Les paramètres inclus sont le « type de balise » (événement personnalisé), « nom d’événement » (clic de bouton) et les « propriétés de l’événement ».][gtm-custom-event]

### Evénements de e-commerce {#ecommerce}

Si votre site enregistre les achats à l’aide de [ l’événement e-commerce] standard, l’élément de couche de données[e-commerce] sur Google Tag Manager, alors vous pouvez utiliser le type de balise **Achat E-commerce**. Ce type d’action enregistre un « achat » séparé dans Braze pour chaque article envoyé dans la liste de `items`.

Vous pouvez également préciser les noms supplémentaires des propriétés que vous souhaitez inclure comme propriétés d’achat en spécifiant leurs clés dans la liste des Propriétés d’achat. Veuillez remarquer que Braze observe la personne `item` qui est enregistrée pour toute propriété d’achat que vous ajoutez à la liste.

Par exemple, imaginons que votre payload e-commerce contient les `items`suivants :

```
items: [{
  item_name: "5 L WIV ECO SAE 5W/30",
  item_id: "10801463",
  price: 24.65,
  item_brand: "EUROLUB",
  quantity: 1
}]
```

Si vous souhaitez transmettre uniquement`item_brand` et `item_name` comme propriétés d’achat, il vous suffit d’ajouter ces deux champs au tableau des propriétés d’achat. Si vous ne fournissez pas de propriété, aucune propriété d’achat n’est envoyée dans l’appel [`logPurchase`][log-purchase] à Braze.

### Suivi des achats {#purchases}

Le type de balise **Achat** appelle la [`logPurchase`méthode](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#logpurchase).

Utilisez cette balise pour suivre les achats avec Braze, y compris, en option, les propriétés d’achat.

Les champs **ID produit** et **Prix** sont obligatoires.

Utilisez le bouton **Ajouter une ligne** pour ajouter les propriétés d’achat.

![Une boîte de dialogue affichant les paramètres de configuration de la balise d’action de Braze. Les paramètres inclus sont les suivants : « type de balise », « ID externe », « prix », « code de devise », « quantité » et « propriétés d’achat »][gtm-purchase]

### Arrêter et reprendre le suivi {#stop-tracking}

Parfois, il se peut que vous deviez désactiver ou réactiver le suivi effectué par Braze sur votre site Internet, par exemple, après qu’un utilisateur a indiqué qu’il refusait le suivi Web pour des raisons de confidentialité.

Utilisez le type de balise **Désactiver le suivi** ou **Redémarrer le suivi** pour désactiver ou réactiver le suivi Web, respectivement.

### Attributs utilisateur personnalisés {#custom-attributes}

Les attributs utilisateur personnalisés ne sont pas disponibles en raison d’une limitation dans la langue de script de Google Tag Manager. Pour enregistrer des attributs personnalisés, créez une balise HTML personnalisée avec le contenu suivant :

```html
<script>
  // note: if using SDK version 3.x or below, use `window.appboy` instead of `window.braze`
  // version 4 or greater should use `window.braze`
window.braze.getUser().setCustomUserAttribute("attribute name", "attribute value");
</script>
```

{% alert important %}
Le modèle GTM ne prend pas en charge les propriétés imbriquées pour les événements ou les achats. Vous pouvez utiliser le code HTML précédent pour enregistrer les événements ou les achats qui nécessitent des propriétés imbriquées.
{% endalert %}

### Attributs utilisateur standards {#standard-attributes}

Les attributs utilisateur standards, tels que le prénom d’un utilisateur, doivent être enregistrés de la même manière que les attributs utilisateur personnalisés. Assurez-vous que les valeurs que vous transmettez pour les attributs standards correspondent au format attendu spécifié dans le document [Classe d’utilisateur][16].

Par exemple, l’attribut genre peut accepter l’un des éléments suivants comme valeurs : "m" | "f" | "o" | "u" | "n" | "p". Par conséquent, pour définir le sexe d’un utilisateur en tant que femme, créez une balise HTML personnalisée avec le contenu suivant :

```html
<script>
window.braze.getUser().setGender("f")
</script>
```

## Mettre à niveau et mettre à jour les modèles {#upgrading}

Pour obtenir la dernière version du SDK Web de Braze, effectuez les trois étapes suivantes dans votre tableau de bord Gestionnaire de balises Google :

1. **Mettre à jour un modèle de balise**<br>Accédez à la page **Modèles** dans votre espace de travail. Vous devez y voir une icône indiquant qu’une mise à jour est disponible.<br><br>![Page des modèles indiquant d’une mise à jour est disponible][gtm-update-available]<br><br>Cliquez sur cette icône et, après avoir étudié la modification, cliquez sur **Accepter la mise à jour**.<br><br>![Un écran comparant l’ancien et le nouveau modèle avec un bouton "Accepter la mise à jour"][gtm-accept-update]<br><br>
2. **Mise à jour du numéro de version**<br>Une fois votre modèle de balise mis à jour, modifiez la balise d’initialisation Braze et mettez à jour la version SDK sur la version la plus récente`major.minor`. Par exemple, si la dernière version est `4.1.2`, saisissez `4.1`. Vous pouvez consulter une liste des versions SDK dans notre [changelog][changelog].<br><br>![Modèle d’initialisation Braze avec un champ de saisie permettant de modifier la version SDK][gtm-version-number]<br><br>
3. **AQ et publication**<br>Vérifiez que la nouvelle version de SDK fonctionne à l’aide de l’outil de débogage Gestionnaire des balises de Google [outil de débogage][gtm-debugging-tool] avant de publier une mise à jour dans votre conteneur de balise.

## Étapes de résolution des problèmes {#troubleshooting}

### Activer le débogage des balises {#debugging}

Chaque modèle de balise de Braze dispose d’une case à cocher facultative **Débogage de balises GTM** qui peut être utilisée pour enregistrer les messages de débogage sur la console JavaScript de votre page Web.

![Outil de débogage du Google Tag Manager][gtm-tag-debugging]

### Entrer dans le mode débogage

Une autre manière de vous aider à déboguer votre intégration Google Tag Manager consiste à utiliser le [Mode Prévisualisation de Google.][14].

Il permet d’identifier les valeurs envoyées à partir de la couche de données de votre page Web vers chaque balise de Braze déclenchée et d’expliquer également quelles balises étaient ou non déclenchées.

![La page de résumé de la balise d’initialisation Braze fournit un aperçu de la balise, y compris des informations sur les balises déclenchées.][gtm-tag-debug-mode]

### Activer la jounalisation verbeuse

Pour permettre à l’assistance technique de Braze de soutenir les journaux d’accès lors du test, vous pouvez activer la journalisation verbeuse sur votre intégration de Google Tag Manager. Ces journaux s’afficheront dans l’onglet **Console** des [outils du développeur de votre navigateur](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools).

Dans votre intégration de Google Tag Manager, accédez à la Balise d’initialisation Braze et sélectionnez **Activer la journalisation SDK Web**.

![La page de résumé de la balise d’initialisation Braze avec l’option Activer la journalisation du SDK Web allumée.][gtm-verbose-logging]

[2]: https://support.google.com/tagmanager/answer/6103696
[gtm-community-gallery-search]: {% image_buster /assets/img/web-gtm/gtm-community-gallery-search.png %}
[gtm-initialization-tag]: {% image_buster /assets/img/web-gtm/gtm-initialization-tag.png %}
[gtm-actions-tag]: {% image_buster /assets/img/web-gtm/gtm-actions-tag.png %}
[6]: {{ site.baseurl }}/user_guide/administrative/app_settings/manage_app_group/app_group_management/#app-group-management
[7]: {{ site.baseurl }}/developer_guide/platform_integration_guides/web/initial_sdk_setup/#step-2-initialize-braze
[gtm-change-user]: {% image_buster /assets/img/web-gtm/gtm-change-user.png %}
[gtm-custom-event]: {% image_buster /assets/img/web-gtm/gtm-custom-event.png %}
[gtm-purchase]: {% image_buster /assets/img/web-gtm/gtm-purchase.png %}
[gtm-tag-debugging]: {% image_buster /assets/img/web-gtm/gtm-tag-debugging.png %}
[gtm-tag-debug-mode]: {% image_buster /assets/img/web-gtm/gtm-debug-mode.png %}
[14]: https://support.google.com/tagmanager/answer/6107056
[15]: https://tagmanager.google.com/gallery/#/?filter=braze
[16]: https://js.appboycdn.com/web-sdk/latest/doc/classes/braze.user.html
[gtm-update-available]: {% image_buster /assets/img/web-gtm/gtm-update-available.png %}
[gtm-accept-update]: {% image_buster /assets/img/web-gtm/gtm-accept-update.png %}
[gtm-version-number]: {% image_buster /assets/img/web-gtm/gtm-version-number.png %}
[changelog]: https://github.com/braze-inc/braze-web-sdk/blob/master/CHANGELOG.md
[gtm-debugging-tool]: https://support.google.com/tagmanager/answer/6107056?hl=en
[e-commerce]: https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm
[log-purchase]: https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#logpurchase
[gtm-verbose-logging]: {% image_buster /assets/img/web-gtm/gtm_verbose_logging.png %}
