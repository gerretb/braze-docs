---
nav_title: Exporter
article_title: Endpoints d’exportation
search_tag: Endpoint
page_order: 2

layout: dev_guide

#Required
description: "Cette page d’accueil explique et répertorie les endpoints Braze d’exportation."
page_type: landing

guide_top_header: "Endpoints d’exportation"
guide_top_text: "Grâce à tous ces endpoints, vous pourrez accéder et exporter différents niveaux de détails sur vos indicateurs clé de performance, cartes de fil d’actualité, sessions d’application, utilisateurs, segments, campagnes et Canvas. <br> <br> Assurez-vous de connaître votre <a href='/docs/user_guide/administrative/access_braze/braze_instances/' target='_blank'>instance Braze</a>, <a href='/docs/api/api_key/' target='_blank'>clé API</a> et <a href='/docs/api/identifier_types/' target='_blank'>identifiant d’API</a> lors de l’élaboration de vos paramètres et corps de requête."

guide_featured_title: "Campagne, Canvas, Fil d’actualité, et Endpoints d’exportation de SMS"
guide_featured_list:
  - name: "GET: Analyse de campagne"
    link: /docs/api/endpoints/export/campaigns/get_campaign_analytics/
    fa_icon: far fa-chart-bar
  - name: "GET: Informations relatives à la campagne"
    link: /docs/api/endpoints/export/campaigns/get_campaign_details/
    fa_icon: far fa-chart-bar
  - name: "GET: Liste des campagnes"
    link: /docs/api/endpoints/export/campaigns/get_campaigns/
    fa_icon: far fa-chart-bar
  - name: "GET: Envoyer des analyses"
    link: /docs/api/endpoints/export/campaigns/get_send_analytics/
    fa_icon: far fa-chart-bar
  - name: "GET: Analyse des séries de données de Canvas"
    link: /docs/api/endpoints/export/canvas/get_canvas_analytics/
    fa_icon: fas fa-project-diagram
  - name: "GET: Résumé de l’analyse des Canvas"
    link: /docs/api/endpoints/export/canvas/get_canvas_analytics_summary/
    fa_icon: fas fa-project-diagram
  - name: "GET: Informations relatives au Canvas"
    link: /docs/api/endpoints/export/canvas/get_canvas_details/
    fa_icon: fas fa-project-diagram
  - name: "GET: Liste des Canvas"
    link: /docs/api/endpoints/export/canvas/get_canvases/
    fa_icon: fas fa-project-diagram
  - name: "GET: Statistiques d’engagement de carte de fil d’actualité"
    link: /docs/api/endpoints/export/news_feed/get_news_feed_card_analytics/
    fa_icon: fas fa-stream
  - name: "GET: Informations relatives à la carte de fil d’actualité"
    link: /docs/api/endpoints/export/news_feed/get_news_feed_card_details/
    fa_icon: fas fa-stream
  - name: "GET: Liste des cartes de fil d’actualité"
    link: /docs/api/endpoints/export/news_feed/get_news_feed_cards/
    fa_icon: fas fa-stream

guide_menu_title: "Événements personnalisés, Indicateurs clé de performance, Achats, Segments, Sessions et Endpoints d’exportation de données utilisateur"
guide_menu_list:
  - name: "GET: Liste des événements personnalisés"
    link: /docs/api/endpoints/export/custom_events/get_custom_events/
    fa_icon: fas fa-chart-line
  - name: "GET: Analyse d’événements personnalisés"
    link: /docs/api/endpoints/export/custom_events/get_custom_events_analytics/
    fa_icon: fas fa-chart-line
  - name: "GET: Indicateurs clé de performance pour les nouveaux utilisateurs quotidiens par date"
    link: /docs/api/endpoints/export/kpi/get_kpi_daily_new_users_date/
    fa_icon: fas fa-bullseye
  - name: "GET: Indicateurs clé de performance pour les utilisateurs actifs quotidiens par date"
    link: /docs/api/endpoints/export/kpi/get_kpi_dau_date/
    fa_icon: fas fa-bullseye
  - name: "GET: Indicateurs clé de performance pour les utilisateurs actifs mensuels au cours des 30 derniers jours"
    link: /docs/api/endpoints/export/kpi/get_kpi_mau_30_days/
    fa_icon: fas fa-bullseye
  - name: "GET: Indicateurs clé de performance pour les désinstallations par date"
    link: /docs/api/endpoints/export/kpi/get_kpi_uninstalls_date/
    fa_icon: fas fa-bullseye
  - name: "GET: Répertorier les ID de produit"
    link: /docs/api/endpoints/export/purchases/get_list_product_id/
    fa_icon: fas fa-list
  - name: "GET: Liste des segments"
    link: /docs/api/endpoints/export/segments/get_segment/
    fa_icon: fas fa-users
  - name: "GET: Analyse des segments"
    link: /docs/api/endpoints/export/segments/get_segment_analytics/
    fa_icon: fas fa-users
  - name: "GET: Informations relatives au segment"
    link: /docs/api/endpoints/export/segments/get_segment_details/
    fa_icon: fas fa-users
  - name: "GET: Données de la série temporelle des sessions App"
    link: /docs/api/endpoints/export/sessions/get_sessions_analytics/
    fa_icon: fas fa-tablet-alt
  - name: "POST: Données utilisateur par identifiant"
    link: /docs/api/endpoints/export/user_data/post_users_identifier/
    fa_icon: fas fa-user
  - name: "POST: Données utilisateur par segment"
    link: /docs/api/endpoints/export/user_data/post_users_segment/
    fa_icon: fas fa-user
  - name: "POST: Données utilisateur par groupe de contrôle global"
    link: /docs/api/endpoints/export/user_data/post_users_global_control_group/
    fa_icon: fas fa-user

---
