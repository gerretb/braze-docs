---
nav_title: "GET : Effectuer une recherche par e-mail d’un compte utilisateur du tableau de bord existant"
article_title: "GET : Effectuer une recherche par e-mail d’un compte utilisateur du tableau de bord existant"
alias: /get_search_existing_dashboard_user_email/
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente des informations concernant l’endpoint Effectuer une recherche par e-mail d’un compte utilisateur du tableau de bord existant."
---

{% api %}
# Effectuer une recherche par e-mail d’un compte utilisateur du tableau de bord existant
{% apimethod get %}
/scim/v2/Users?filter=userName eq "user@test.com"
{% endapimethod %}

Cet endpoint vous permet de rechercher un compte utilisateur du tableau de bord existant en spécifiant leur e-mail dans les paramètres du filtre de recherche. Veuillez prendre en compte que, lorsque le paramètre de recherche est encodé par URL, il s’affichera ainsi :

`/scim/v2/Users?filter=userName%20eq%20%22user@test.com%22`

Pour plus d’informations sur la manière d’obtenir un jeton SCIM, consultez [Automated user provisioning]({{site.baseurl}}/scim/automated_user_provisioning/). (Approvisionnement automatisé des utilisateurs).

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#5037d810-b822-4c54-bb51-f30470a42a95 {% endapiref %}

## Limites de débit

{% multi_lang_include rate_limits.md endpoint='look up dashboard user email' %}

## Exemple de demande
```json
curl --location --request GET \ 'https://rest.iad-01.braze.com/scim/v2/Users?filter=userName%20eq%20%22user@test.com%22' \
--header 'Content-Type: application/json' \
--header 'X-Request-Origin: YOUR-REQUEST-ORIGIN-HERE' \
--header 'Authorization: Bearer YOUR-SCIM-TOKEN-HERE' \
```

## Réponse
```json
Content-Type: application/json
X-Request-Origin: YOUR-REQUEST-ORIGIN-HERE
Authorization: Bearer YOUR-SCIM-TOKEN-HERE
{
    "schemas": ["urn:ietf:params:scim:api:messages:2.0:ListResponse"],
    "totalResults": 1,
    "Resources": [
        {
            "userName": "user@test.com",
            "id": "dfa245b7-24195aec-887bb3ad-602b3340",
            "name": {
                "givenName": "Test",
                "familyName": "Utilisateur"
            },
            "department": "finance",
            "lastSignInAt": "Mardi 1er janvier, 1970 12:00:00 AM",
            "permissions": {
                "companyPermissions": ["manage_company_settings"],
                "appGroup": [
                    {
                        "appGroupId": "241adcd25789fabcded",
                        "appGroupName": "Groupe d’apps de test",
                        "appGroupPermissions": ["basic_access","send_campaigns_canvases"],
                        "team": [
                            {
                                "teamId": "241adcd25789fabcded",
                                "teamName": "Test Team",                  
                                "teamPermissions": ["admin"]
                            }
                        ]
                    } 
                ]
            }
        }
    ]
}
```

{% endapi %}

