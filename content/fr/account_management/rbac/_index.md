---
aliases:
- /fr/guides/rbac
- /fr/account_management/rbac/role_api
- /fr/account_management/users/default_roles
- /fr/account_management/users/custom_roles
- /fr/account_management/rbac/log_management
further_reading:
- link: /api/v2/roles/
  tag: Documentation
  text: Gérer les rôles et les autorisations avec l’API Roles
- link: /api/v2/roles/#enumerer-les-autorisations
  tag: Documentation
  text: Gérer vos autorisations avec l'API Permissions
- link: /account_management/rbac/permissions
  tag: Documentation
  text: Découvrir la liste des permissions disponibles
- link: /account_management/saml/
  tag: Documentation
  text: Activer l'authentification unique avec SAML
- link: https://www.datadoghq.com/blog/compliance-governance-transparency-with-datadog-audit-trail/
  tag: Blog
  text: Concevoir une stratégie de conformité, gouvernance et transparence pour toutes
    vos équipes avec le journal d'audit Datadog
kind: documentation
title: Contrôle d'accès à base de rôles (RBAC)
---

Les rôles permettent de classifier les utilisateurs et de définir les autorisations d'accès qu'ils possèdent. Vous pouvez ainsi choisir le type de données qu'ils peuvent lire ou encore le type de ressources de compte qu'ils peuvent modifier. Par défaut, Datadog propose trois rôles. Vous pouvez cependant créer des [rôles personnalisés](#rôles-personnalisés) afin de vous assurer que vos utilisateurs possèdent le bon niveau d'autorisation.

Lorsque vous attribuez des autorisations à un rôle, tous les utilisateurs associés à ce rôle bénéficient de ces autorisations. Lorsque les utilisateurs sont associés à plusieurs rôles, ils bénéficient de l'ensemble des autorisations correspondant à chacun de ces rôles. Plus un utilisateur dispose de rôles, plus il peut accéder aux différentes fonctionnalités d'un compte Datadog.

Si un utilisateur dans une [organisation enfant][1] dispose de l'autorisation `org_management`, cela ne signifie pas que c'est aussi le cas dans l'organisation parente. Les rôles des utilisateurs ne sont pas partagés entre les organisations parent et enfant.

**Remarque** : si vous avez recours à un fournisseur d'identité SAML, vous pouvez l'intégrer à Datadog pour l'authentification et mapper des attributs d'identité à des rôles Datadog par défaut ou personnalisés. Consultez la section [Authentification unique avec SAML][2] pour en savoir plus.

## Rôles Datadog par défaut

Rôle Admin Datadog
: Utilisateurs ayant accès aux informations de facturation, autorisés à révoquer des clés API et capables de gérer des utilisateurs et de configurer [des dashboards en lecture seule][3]. Ils peuvent également accorder le rôle d'administrateur à un utilisateur standard.
 

Rôle Standard Datadog
: Utilisateurs autorisés à consulter et à modifier toutes les fonctionnalités de surveillance offertes par Datadog, telles que les [dashboards][3], les [monitors][4], les [événements][5] et les [notebooks][6]. Ils peuvent également inviter d'autres utilisateurs à rejoindre une organisation.

Rôle Read-Only Datadog
: Utilisateurs n'ayant aucun droit de modification dans Datadog. Ce rôle est particulièrement utile lorsque vous souhaitez partager des vues spécifiques en lecture seule avec un client ou lorsqu'un membre d'un service souhaite partager un [dashboard][3] avec une personne d'un autre service.

## Rôles personnalisés

Les rôles personnalisés offrent à votre organisation la possibilité de créer des rôles dotés d'autorisations uniques. Gérez vos rôles personnalisés sur le site de Datadog, avec l'[API Role Datadog][7] ou directement via SAML. Poursuivez votre lecture pour découvrir comment créer, mettre à jour et supprimer un rôle. Consultez la section [Autorisations des rôles Datadog][8] pour en savoir plus sur les autorisations disponibles. Seuls les utilisateurs disposant de l'autorisation User Access Management peuvent créer ou modifier des rôles dans Datadog.

### Activer les rôles personnalisés

1. Accédez aux [Paramètres d'organisation][9]. 
2. À gauche de la page, sélectionnez **Roles**.
3. Cliquez sur l'icône en forme d'engrenage en haut à droite. La fenêtre contextuelle Custom Roles s'affiche alors.
4. Dans la fenêtre contextuelle Custom Roles, cliquez sur **Enable** pour activer la fonctionnalité.

{{< img src="account_management/rbac/enable_custom_roles.png" alt="Fenêtre contextuelle des rôles personnalisés avec bouton d'activation" style="width:90%;">}}

Vous pouvez également effectuer un appel POST sur l'[endpoint d'API Create Role][10] afin d'activer automatiquement les rôles personnalisés pour votre organisation.

### Créer un rôle personnalisé

{{< tabs >}}
{{% tab "Application Datadog" %}}

Pour créer un rôle personnalisé :

1. Accédez à votre [page Roles sur Datadog][1].
2. Sélectionnez **New Role** en haut à droite.
3. Attribuez un nom à votre rôle.
4. Attribuez un ensemble d'autorisations à votre rôle. Consultez la section [Autorisations des rôles Datadog][2] pour en savoir plus sur les autorisations disponibles.

Une fois votre rôle créé, vous pouvez l'[ajouter à des utilisateurs existants][3].


[1]: https://app.datadoghq.com/access/roles
[2]: /fr/account_management/rbac/permissions/
[3]: /fr/account_management/users/#edit-a-user-roles
{{% /tab %}}
{{% tab "API" %}}

Pour découvrir un exemple de création de rôle avec l'API, consultez la [documentation à ce sujet][1].


[1]: /fr/api/latest/roles/#create-role
{{% /tab %}}
{{< /tabs >}}

### Mettre à jour un rôle

{{< tabs >}}
{{% tab "Application Datadog" %}}

Pour modifier un rôle personnalisé :

1. Accédez à votre [page Roles sur Datadog][1].
2. Sélectionnez le bouton de modification pour le rôle de votre choix.
3. Modifiez l'ensemble d'autorisations de votre rôle. Consultez la section [Autorisations des rôles Datadog][2] pour en savoir plus sur les autorisations disponibles.
4. Enregistrez vos modifications.


Une fois votre rôle modifié, les autorisations sont mises à jour pour l'ensemble des utilisateurs qui disposent de ce rôle.


[1]: https://app.datadoghq.com/access/roles
[2]: /fr/account_management/rbac/permissions/
{{% /tab %}}
{{% tab "API" %}}

Pour découvrir un exemple de mise à jour de rôle avec l'API, consultez la [documentation à ce sujet][1].


[1]: /fr/api/latest/roles/#update-a-role
{{% /tab %}}
{{< /tabs >}}

### Dupliquer un rôle

{{< tabs >}}
{{% tab "Application Datadog" %}}

Pour dupliquer un rôle existant :

1. Accédez à votre [page Roles sur Datadog][1].
2. Passez votre curseur sur le rôle que vous souhaitez dupliquer. Plusieurs boutons apparaissent sur la droite.
3. Sélectionnez le bouton de duplication pour le rôle de votre choix.
4. Si besoin, modifiez le nom ou les autorisations du rôle.
5. Cliquez sur le bouton **Save** en bas.

{{< img src="account_management/rbac/clone_role.png" alt="Liste de deux rôles avec le bouton de duplication mis en évidence" style="width:90%;">}}


[1]: https://app.datadoghq.com/access/roles
{{% /tab %}}
{{% tab "API" %}}

Pour découvrir un exemple de duplication de rôle avec l'API, consultez la [documentation à ce sujet][1].

[1]: /fr/api/latest/roles/#create-a-new-role-by-cloning-an-existing-role
{{% /tab %}}
{{< /tabs >}}

### Supprimer un rôle

{{< tabs >}}
{{% tab "Application Datadog" %}}

Pour supprimer un rôle personnalisé :

1. Accédez à votre [page Roles sur Datadog][1].
2. Passez votre curseur sur le rôle que vous souhaitez supprimer. Plusieurs boutons apparaissent sur la droite.
3. Sélectionnez le bouton de suppression pour le rôle de votre choix.
4. Confirmez l'action.


Une fois votre rôle supprimé, les autorisations sont mises à jour pour tous les utilisateurs qui disposent de ce rôle. Les utilisateurs sans autre rôle ne peuvent pas exploiter toutes les fonctionnalités de Datadog, mais conservent un accès limité.


[1]: https://app.datadoghq.com/access/roles
{{% /tab %}}
{{% tab "API" %}}

Pour découvrir un exemple de suppression de rôle avec l'API, consultez la [documentation à ce sujet][1].


[1]: /fr/api/latest/roles/#delete-role
{{% /tab %}}
{{< /tabs >}}

### Appliquer un modèle de rôle

Lorsque vous créez ou mettez à jour un rôle sur le site de Datadog, vous pouvez utiliser un modèle de rôle pour appliquer un ensemble prédéfini d'autorisations au rôle.

1. Sur la page de création ou de modification d'un rôle, cliquez sur le bouton **Show Role Templates** à droite.
2. Un menu déroulant apparaît avec les différents modèles de rôle.
3. Depuis le menu, sélectionnez le modèle de rôle dont vous souhaitez appliquer les autorisations.
4. Cliquez sur le bouton **Apply**.
4. Apportez d'autres modifications à votre rôle si vous le souhaitez.
5. Cliquez sur le bouton **Save**.

{{< img src="account_management/rbac/role_templates.png" alt="Menu déroulant des modèles de rôle avec le rôle Datadog Billing Admin sélectionné" style="width:90%;">}}

## Restreindre l'accès à des ressources spécifiques (contrôles d'accès granulaires)

Vous avez la possibilité de limiter l'accès à certaines ressources à des rôles, [équipes][16] (bêta) ou utilisateurs (bêta) spécifiques. Datadog vous recommande d'utiliser des équipes pour accorder des accès à des groupes fonctionnels au sein de votre organisation (par exemple, rendre la modification d'un dashboard possible uniquement par l'équipe qui en est propriétaire), des rôles pour accorder des accès à des types d'utilisateurs (par exemple, rendre la modification des moyens de paiement possible uniquement par les responsables de la facturation), et des utilisateurs individuels uniquement lorsque cela est nécessaire. Ce mode de fonctionnement encourage le partage des connaissances et la collaboration.


| Ressources compatibles avec les contrôles d'accès granulaires | Accès par équipe | Accès par rôle | Accès par utilisateur / compte de service |
|--------------------------------------------------|-------------------|-------------------|-------------------------------------|
| [Dashboards][11]                                 | {{< X >}}         | {{< X >}}         | {{< X >}}                           |
| [Monitors][12]                                   |                   | {{< X >}}         |                                     |
| [Notebooks][6]                                   | {{< X >}}         | {{< X >}}         | {{< X >}}                           |
| [Règles de sécurité][13]                             | {{< X >}}         | {{< X >}}         | {{< X >}}                           |
| [Service Level Objectives][14]                   | {{< X >}}         | {{< X >}}         | {{< X >}}                           |
| [Tests Synthetic][15]                            |                   | {{< X >}}         |                                     |


## Pour aller plus loin

{{< partial name="whats-next/whats-next.html" >}}

[1]: /fr/account_management/multi_organization/
[2]: /fr/account_management/saml/
[3]: /fr/dashboards/
[4]: /fr/monitors/
[5]: /fr/events/
[6]: /fr/notebooks/#limit-edit-access
[7]: /fr/api/v2/roles/
[8]: /fr/account_management/rbac/permissions/
[9]: https://app.datadoghq.com/organization-settings/
[10]: /fr/api/latest/roles/#create-role
[11]: /fr/dashboards/#permissions
[12]: /fr/monitors/notify/#permissions
[13]: /fr/security/detection_rules/#limit-edit-access
[14]: /fr/service_management/service_level_objectives/#permissions
[15]: /fr/synthetics/browser_tests/#permissions
[16]: /fr/account_management/teams/