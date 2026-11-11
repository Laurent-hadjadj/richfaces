# Journal des modifications

Ce fichier liste les modifications de ce **fork** de RichFaces 4.5.17.Final par rapport à la dernière version du projet d'origine (4.5.17.Final). Le projet d'origine est en fin de vie depuis 2016.

Le fork est distribué sous la licence d'origine, **LGPL v2.1** (voir `lgpl.txt` et `NOTICE.txt`). Il n'est ni affilié ni approuvé par Red Hat, JBoss ou le projet RichFaces d'origine.

Les notes de version historiques du projet d'origine (en anglais) sont dans `dist/src/main/resources/txt/release-notes.txt`.

## [4.5.18] — 11 novembre 2026

Version corrective de sécurité. Elle contient **uniquement** les changements ci-dessous : aucune dépendance, bibliothèque embarquée ou composant n'est mis à jour.

### Sécurité

- **Suppression du composant `a4j:mediaOutput`** — corrige la [CVE-2018-12532](https://nvd.nist.gov/vuln/detail/CVE-2018-12532).
  Supprime le composant, son rendu, sa ressource (`MediaOutputResource`), son handler Facelets, sa déclaration de balise, ses tests et ses exemples du showcase.
  Report du commit `dff8da749` (2018-08-21) d'**Alberto Fernandez** dans [albfernandez/richfaces](https://github.com/albfernandez/richfaces).
- **Suppression de la sérialisation et de la désérialisation des données de ressource** (paramètre d'URL `do`).
  L'état d'une ressource n'est plus transmis qu'en octets (`db`). Supprime `LookAheadObjectInputStream`, sa liste blanche de classes (`resource-serialization.properties`) et le chemin « objet » de `ResourceUtils`.
  Dans la 4.5.17.Final, le paramètre `do` était décodé pour toute requête de ressource valide, n'était ni chiffré ni signé, et n'était protégé que par une liste blanche de classes.
  Report du commit `ba2a98a49` (2018-11-17) de **Kyle Stiemann**, issu du même fork.

### Changements incompatibles

- Les pages qui utilisent `<a4j:mediaOutput>` ne fonctionnent plus et doivent être adaptées avant la mise à jour.
- Les ressources personnalisées qui implémentent `javax.faces.component.StateHolder` (et s'appuient sur le paramètre `do`) ne sont plus prises en charge.

### Compilation

- `version.cdk` est remis à la version publiée `4.5.0.Final` (c'était `4.5.1-SNAPSHOT`, une version de développement jamais publiée, dans la branche de développement du projet d'origine). Le CDK `4.5.0.Final` est publié sur le [dépôt public JBoss](https://repository.jboss.org/nexus/content/groups/public/), et non sur Maven Central.

### Non corrigé / non inclus

- **RichFaces 3.x** n'est pas couvert (ce fork ne concerne que la branche 4.5).
- **Les bibliothèques embarquées sont inchangées** : jQuery 1.12.3 et CKEditor 4.5.8, telles qu'incluses dans la 4.5.17.Final. Les vulnérabilités publiées pour ces versions ne sont pas traitées.
- **Aucun autre correctif de vulnérabilité.** Situation des autres CVE RichFaces, d'après les bases publiques consultées le 2026-11-11 (NVD, Red Hat, avis GitLab et OSV ; les sources divergent parfois sur les bornes exactes) :
  - CVE-2018-12532 : versions 4.5.3 à 4.5.17, aucun correctif amont connu ; corrigée par cette version.
  - CVE-2015-0279 : versions 4.0.0 à 4.5.4, corrigée avant la 4.5.17.Final. La CVE-2018-12532 est un contournement de son correctif.
  - CVE-2013-2165 (désérialisation) : corrigée en 4.3.2 ou 4.3.3 selon les sources, donc dans la 4.5.17.Final.
  - CVE-2014-0086 (déni de service) : versions 4.3.4 à 4.3.5 et préversions 5.0.0, corrigée en 4.3.6. Ne concerne pas la 4.5.
  - CVE-2018-12533 et CVE-2018-14667 : ne concernent que RichFaces 3.x jusqu'à 3.3.4, pas la 4.5. Une application restée en RichFaces 3.x n'est pas protégée par cette version.
- **CVE d'Hibernate Validator associées à RichFaces par certains outils** (CVE-2025-35036, CVE-2023-1932, CVE-2020-10693) : ce ne sont pas des vulnérabilités du code RichFaces. Le POM ne déclare `hibernate-validator` qu'en portée `test`, donc non transmis aux applications. Cette version ne modifie rien à ce sujet ; une application qui utilise elle-même Hibernate Validator doit le mettre à jour de son côté.
- Les autres usages de la sérialisation Java dans le code (par exemple l'état de vue JSF) ne sont pas modifiés.
- Aucune nouvelle fonctionnalité et aucune mise à jour de compatibilité (implémentations JSF, serveurs d'applications, navigateurs).
- Cette version n'a **pas** fait l'objet d'un audit de sécurité indépendant.

## [4.5.17.Final]

Dernière version du projet d'origine. Voir `dist/src/main/resources/txt/release-notes.txt`.
