# 🛡️ RichFaces 4.5.18 — version corrective de sécurité (fork de la 4.5.17.Final)

> [!NOTE]
> 🍴 Ce dépôt est un **fork** de RichFaces **4.5.17.Final**, dernière version de la branche 4.5 publiée par le projet d'origine. RichFaces est en fin de vie depuis 2016 et le projet d'origine ne fournit plus de correctifs de sécurité.\
> 🚫 Ce fork n'est **ni affilié ni approuvé** par Red Hat, JBoss ou le projet RichFaces d'origine.\
> 🔗 Le projet d'origine est disponible sur [github.com/richfaces/richfaces](https://github.com/richfaces/richfaces).

## 1️⃣ 📜 Licence

Ce fork est distribué sous la **licence d'origine : LGPL v2.1** (voir `lgpl.txt` et `NOTICE.txt`). Les en-têtes de copyright et de licence des fichiers sources d'origine sont **inchangés**. Les modifications apportées à la 4.5.17.Final sont listées ci-dessous et dans le [CHANGELOG.md](CHANGELOG.md).

## 2️⃣ 🩹 Ce que corrige la 4.5.18

La 4.5.18 contient **uniquement** les changements suivants par rapport à la 4.5.17.Final. Aucune dépendance, aucune bibliothèque embarquée et aucun composant n'est mis à jour.

- 🔴➡️🟢 **CVE-2018-12532** : le composant `a4j:mediaOutput` est **supprimé** (composant, rendu, ressource, handler Facelets et déclaration de balise).
- 🔐 **Suppression de la sérialisation de l'état des ressources** : le paramètre d'URL `do` (objet Java sérialisé) n'est plus produit ni décodé. L'état d'une ressource n'est plus transmis qu'en octets (`db`). La classe `LookAheadObjectInputStream` et sa liste blanche sont supprimées. Dans la 4.5.17.Final, ce paramètre était décodé pour toute requête de ressource valide, n'était ni chiffré ni signé, et n'était protégé que par une liste blanche de classes.

## 3️⃣ ⚠️ Changements incompatibles

- 💥 Les pages qui utilisent `<a4j:mediaOutput>` **ne fonctionnent plus** et doivent être adaptées avant la mise à jour.
- 💥 Les ressources personnalisées qui implémentent `javax.faces.component.StateHolder` (et s'appuient sur le paramètre `do`) **ne sont plus prises en charge**.

## 4️⃣ 🚫 Ce que la 4.5.18 ne corrige PAS

> [!WARNING]
> 🕸️ **RichFaces 3.x n'est pas couvert.** Ce fork ne concerne que la branche 4.5 : une application restée en RichFaces 3.x **n'est pas protégée** par cette version.

- 📦 **Les bibliothèques tierces embarquées sont inchangées** (telles qu'incluses dans la 4.5.17.Final) : jQuery 1.12.3 et CKEditor 4.5.8. Les vulnérabilités publiées pour ces versions ne sont **pas** traitées.
- 🔎 **Aucun autre correctif de vulnérabilité n'est inclus.** Situation des autres CVE RichFaces, d'après les bases publiques consultées le 2026-11-11 (NVD, Red Hat, avis GitLab et OSV ; les sources divergent parfois sur les bornes exactes) :

| CVE | Versions affectées | Statut avec la 4.5.18 |
| --- | --- | --- |
| [CVE-2018-12532](https://nvd.nist.gov/vuln/detail/CVE-2018-12532) | 4.5.3 à 4.5.17 ; **aucun correctif amont connu** | ✅ **Corrigée** par la 4.5.18 (retrait de `mediaOutput`) |
| [CVE-2015-0279](https://nvd.nist.gov/vuln/detail/CVE-2015-0279) | 4.0.0 à 4.5.4 | ✅ Corrigée avant la 4.5.17.Final (la CVE-2018-12532 en est un **contournement**) |
| [CVE-2013-2165](https://nvd.nist.gov/vuln/detail/CVE-2013-2165) (désérialisation) | 4.0.0 à 4.3.2 (3.x : avant 3.3.4) ; borne 4.3.2 ou 4.3.3 selon les sources | ✅ Corrigée avant la 4.5.17.Final |
| [CVE-2014-0086](https://nvd.nist.gov/vuln/detail/CVE-2014-0086) (déni de service) | 4.3.4 à 4.3.5 et préversions 5.0.0 | ✅ **Ne concerne pas la 4.5** (corrigée en 4.3.6) |
| [CVE-2018-12533](https://nvd.nist.gov/vuln/detail/CVE-2018-12533) | **3.1.0 à 3.3.4 uniquement** | ℹ️ Ne concerne pas la 4.x ; une application en RichFaces 3.x n'est **pas** protégée |
| [CVE-2018-14667](https://nvd.nist.gov/vuln/detail/CVE-2018-14667) | **3.x jusqu'à 3.3.4 uniquement** | ℹ️ Ne concerne pas la 4.x ; une application en RichFaces 3.x n'est **pas** protégée |

- 🗄️ **CVE d'Hibernate Validator associées à RichFaces par certains outils.** Des outils d'analyse (par exemple l'onglet des vulnérabilités de Maven Central) peuvent associer à `org.richfaces:richfaces` 4.5.17.Final des CVE d'Hibernate Validator (CVE-2025-35036, CVE-2023-1932, CVE-2020-10693). Ce ne sont pas des vulnérabilités du code RichFaces : le POM ne déclare `hibernate-validator` qu'en portée `test`, donc non transmis aux applications qui utilisent RichFaces. Cette version ne modifie rien à ce sujet. Une application qui utilise elle-même Hibernate Validator doit le mettre à jour de son côté.
- ♻️ Les autres usages de la sérialisation Java dans le code (par exemple l'état de vue JSF) ne sont pas modifiés.
- 🚧 Aucune nouvelle fonctionnalité, aucune mise à jour de compatibilité (implémentations JSF, serveurs d'applications, navigateurs).
- 🧪 Cette version **n'a pas fait l'objet d'un audit de sécurité indépendant**. Validez-la dans votre propre environnement avant de l'utiliser.

## 5️⃣ 🤝 Crédits

Les changements de sécurité sont des **reports** (*backports*) de travaux publiés dans le fork [albfernandez/richfaces](https://github.com/albfernandez/richfaces) :

- 👤 **Alberto Fernandez** : suppression de `a4j:mediaOutput` (CVE-2018-12532), commit `dff8da749` (2018-08-21).
- 👤 **Kyle Stiemann** : suppression de la sérialisation et de la désérialisation des données de ressource, commit `ba2a98a49` (2018-11-17).

Le code RichFaces d'origine est l'œuvre de Red Hat, de JBoss et des contributeurs de RichFaces.
Le report sur la 4.5.17.Final et la correction du build ont été réalisés par 👤**Laurent Hadjadj**.

## 6️⃣ 🔨 Compilation de cette version

La compilation utilise le CDK publié `org.richfaces.cdk:*:4.5.0.Final`, comme la 4.5.17.Final. La branche de développement du projet d'origine référençait le CDK `4.5.1-SNAPSHOT`, jamais publié : ce fork le remet à `4.5.0.Final`.

Le CDK `4.5.0.Final` **n'est pas disponible sur Maven Central**. Il est publié sur le [dépôt public JBoss](https://repository.jboss.org/nexus/content/groups/public/), qui doit être accessible depuis votre configuration Maven.

## 7️⃣ 📚 Documentation d'origine

Le guide de démarrage, les instructions de compilation détaillées et la documentation de contribution du projet d'origine (en anglais) restent dans [README-origine.adoc](README-origine.adoc) et [CONTRIBUTING.md](CONTRIBUTING.md).
