# Exercice 04 – Docker Compose

Dans cet exercice, tu vas déployer trois sites web en utilisant Docker Compose. Les sites à déployer sont :

* [Grimoire] (port 81)
* [HedgeDoc] (port 82)
* [Planka] (port 83)

![Aperçu](.docs/preview.png)

## Travail à faire 

Tu trouveras dans ce dépôt un dossier pour chaque site à déployer. Tu dois placer dans ces dossiers les fichiers
`docker-compose.yml` et `.env` de chaque site demandé. C'est ce que tu dois remettre pour cet exercice.

> [!NOTE]
> Au fur et à mesure de l’exercice, les consignes seront de moins en moins détaillées. L’objectif est de t’amener 
> progressivement à chercher par toi-même les informations nécessaires dans la documentation en ligne.

> [!WARNING]
> Fais attention à ne pas envoyer sur le dépôt les fichiers générés par les conteneurs. Pour cela, ajoute dans chaque
> dossier un fichier `.gitignore` listant les dossiers à ignorer (en pratique, il s’agit généralement des volumes des 
> conteneurs). Ce sera noté durant la correction de l'exercice.

## Service 1 – Grimoire

Commence par déployer un serveur [Grimoire]. Il s'agit d'une application où il est possible d'écrire des recettes.

<table width="100%">
  <tr>
    <th>Image</th>
    <th>Ports</th>
    <th>Volumes</th>
    <th>Variables d'environnement</th>
    <th>Dépendances</th>
  </tr>
  <tr>
    <td>
      <code>blemelin/grimoire</code>
    </td>
    <td>
      <code>81</code> ➔ <code>8242</code>
    </td>
    <td>
      <code>/grimoire/data</code>
    </td>
    <td>
      --
    </td>
    <td>
      --
    </td>
  </tr>
</table>

À partir du tableau ci-dessus et de la [documentation][Grimoire], rédige le fichier `docker-compose.yml` (et son fichier
`.env`) permettant de lancer le [Grimoire]. Exécute l'application et vérifie que cela marche.

> [!WARNING]
> N'oublie pas les autres rubriques, tel que `container_name`, `depends_on` et `restart` (si applicables).

## Service 2 – HedgeDoc

Déploie un serveur [HedgeDoc]. Il s'agit d'un éditeur collaboratif de Markdown.

<table width="100%">
  <tr>
    <th>Image</th>
    <th>Ports</th>
    <th>Volumes</th>
    <th>Variables d'environnement</th>
    <th>Dépendances</th>
  </tr>
  <tr>
    <td>
      <code>quay.io/hedgedoc/hedgedoc:1.10.6</code>
    </td>
    <td>
      <code>82</code> ➔ <code>3000</code>
    </td>
    <td>
      <code>/hedgedoc/public/uploads</code>
    </td>
    <td>
      <code>CMD_DB_URL</code><br>
      <code>CMD_CSP_ENABLE</code><br>
    </td>
    <td>
      <code>postgres</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>postgres:17.7-alpine</code>
    </td>
    <td>
      --
    </td>
    <td>
      <code>/var/lib/postgresql/data</code>
    </td>
    <td>
      <code>POSTGRES_DB</code><br>
      <code>POSTGRES_USER</code><br>
      <code>POSTGRES_PASSWORD</code><br>
    </td>
    <td>
      --
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <th colspan="2">Variables d'environnement de HedgeDoc</th>
  </tr>
  <tr>
    <td><code>CMD_DB_URL</code></td>
    <td>
      <code>postgres://&lt;USER&gt;:&lt;PASSWORD&gt;@&lt;HOST&gt;:5432/&lt;DATABASE&gt;</code><br><br>
      Où :
      <ul>
        <li><code>&lt;USER&gt;</code> est le nom d'utilisateur de la base de données.</li>
        <li><code>&lt;PASSWORD&gt;</code> est le mot de passe de la base de données.</li>
        <li><code>&lt;HOST&gt;</code> est le nom d'hôte de la base de données.</li>
        <li><code>&lt;DATABASE&gt;</code> est le nom de la base de données.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td><code>CMD_CSP_ENABLE</code></td>
    <td><code>false</code></td>
  </tr>
  <tr>
    <th colspan="2">Variables d'environnement de PostgreSQL</th>
  </tr>
  <tr>
    <td><code>POSTGRES_DB</code></td>
    <td><code>hedgedoc</code></td>
  </tr>
  <tr>
    <td><code>POSTGRES_USER</code></td>
    <td><code>hedgedoc</code></td>
  </tr>
  <tr>
    <td><code>POSTGRES_PASSWORD</code></td>
    <td>Un mot de passe aléatoire</td>
  </tr>
</table>

À partir des deux tableaux ci-dessus et de la [documentation][HedgeDoc], rédige le fichier `docker-compose.yml` (et son 
fichier `.env`) pour cette application. Exécute l'application et vérifie que cela marche.

> [!IMPORTANT]
> Plusieurs variables d'environnement se répètent dans cette application. Utilise bien le fichier `.env` afin d'éviter
> de *copier-coller* des valeurs dans ton fichier `docker-compose.yml`.

> [!WARNING]
> PostgreSQL risque de ne pas être prêt au moment où l'application démarre. Tu dois gérer cette situation.

## Service 3 – Planka

Déploie un serveur [Planka]. Il s'agit d'une plateforme pour créer des tableaux Kanban.

<table width="100%">
  <tr>
    <th>Image</th>
    <th>Ports</th>
    <th>Volumes</th>
    <th>Variables d'environnement</th>
    <th>Dépendances</th>
  </tr>
  <tr>
    <td>
      <code>ghcr.io/plankanban/planka</code>
    </td>
    <td>
      <code>83</code> ➔ <code>1337</code>
    </td>
    <td>
      ??
    </td>
    <td>
      ??
    </td>
    <td>
      ??
    </td>
  </tr>
  <tr>
    <td>
      <code>postgres:16-alpine</code>
    </td>
    <td>
      ??
    </td>
    <td>
      ??
    </td>
    <td>
      ??
    </td>
    <td>
      ??
    </td>
  </tr>
</table>

À partir des deux tableaux ci-dessus et de la [documentation][Planka], rédige le fichier `docker-compose.yml` (et son 
fichier `.env`) pour cette application. Exécute l'application et vérifie que cela marche. Cette fois, tu dois te 
connecter au compte administrateur de l'application.

> [!CAUTION]
> Cette fois, la plupart des informations sont manquantes. À toi de les trouver dans la [documentation][Planka]. 
> Pour t'aider, inspire-toi de ce que tu as fai pour l'application précédente : de nombreux détails sont similaires.
>
> À noter que la [documentation][Planka] te conseille un mécanisme d'authentification différent pour la base de 
> données que ce qui a été fait précédemment. Tu n'es absolument pas obligé de procéder ainsi : tu peux faire exactement
> comme pour [HedgeDoc].
>
> Remarque aussi que la documentation contient un fichier `docker-compose.yml` en guise de point de départ. Tu aura à
> l'adapter à ta situation. Par exemple, il utilise des volumes nommés, mais il vous est demandé de toujours utiliser
> la méthode plus simple montrée en classe.

## Modalités de remise

Remets ton projet sur GitHub Classroom. N'oublie pas de faire un commit, un push et de vérifier sur le site de GitHub 
que tous tes fichiers ont bien été téléversés.

[Grimoire]: https://hub.docker.com/r/blemelin/grimoire
[HedgeDoc]: https://hedgedoc.org/
[Planka]: https://docs.planka.cloud/docs/welcome

# Travail Pratique 2 – Docker et Docker Compose

Dans ce travail pratique, tu devras déployer plusieurs applications web en utilisant Docker et Docker Compose. Certaines
applications devront être déployées à l'aide de simples commandes `docker run`, et d'autres à l'aide d'un fichier 
`compose.yaml` (et son fichier `.env` qui l'accompagne).

Contrairement aux exercices, tu devras consulter la **documentation officielle de chaque application** afin de trouver :

* l'image Docker à utiliser
* les ports à exposer
* les volumes à configurer
* les variables d'environnement nécessaires

## Conditions de réalisation

- **Valeur de la note finale** : 20%
- **Contexte de réalisation** : Individuel
- **Durée** : 1 ½ semaine
- **Utilisation de l'iAG** : Niveau 1 - Toi qui complètes (assistance à la rédaction)

## Tâches à réaliser

Tu trouveras dans ce dépôt un dossier pour chaque site à déployer. Tu dois placer dans ces dossiers :

- Un fichier `deploy.sh` pour les applications déployées avec `docker run`.
- Un fichier `compose.yaml` et `.env` pour les applications déployées avec `docker compose up`.

Dès le début du travail, crée une branche `dev` à partir de la branche `main`. À la fin du travail, tu devras fusionner
la branche `dev` dans la branche `main` pour confirmer que tu as remis le travail. Chaque partie du travail devra être 
réalisée dans sa propre feature-branch (le nom de la branche te sera indiqué). Ces branches devront être fusionnées dans
la branche `dev` pour confirmer que que tu as terminé la partie en cours. Ne supprime pas les branches : elles seront 
utilisées lors de la correction.

### Partie 1 : Déploiement avec `docker run`

Pour chaque application dans cette partie, rédige un fichier `deploy.sh` contenant une commande `docker run` pour
déployer et exécuter l'application. Inclus aussi dans ce fichier la création de tout ce qui est nécessaire à l'exécution
de la commande (création de dossiers, d'utilisateurs, modifications de droits d'accès, etc).

Dans tous les cas :

- Les applications doivent s'exécuter en arrière-plan, pas de manière interactive.
- Les applications doivent s'exécuter avec les privilèges de l'utilisateur `student`, si c'est possible.
- Les fichiers de l'application doivent être dans le dossier `/srv/nom-de-application`.

#### Application 1 - Memos (`feat/memos`)

Déploie une instance de [Memos], une application de notes légère pour capturer et partager des idées. L'application doit
s'exécuter sur le port `81`.

![Memos](.docs/memos.png)

#### Application 2 - Opengist (`feat/opengist`)

Déploie une instance de [Opengist], une application de type *pastebin* basée sur Git. L'application doit s'exécuter sur le
port `82`.

![Opengist](.docs/opengist.png)

### Partie 2 : Déploiement avec `docker compose`

Pour chaque application dans cette partie, rédige un fichier `compose.yaml` (et son fichier `.env`) pour déployer 
et exécuter l'application. Inclus aussi un fichier `deploy.sh` créant tout ce qui est nécessaire à l'exécution de
l'application (incluant la commande `docker compose` déclenchant l'exécution de l'application).

Dans tous les cas :

- Les applications doivent s'exécuter en arrière-plan, pas de manière interactive.
- Les applications doivent s'exécuter avec les privilèges de l'utilisateur `student`, si c'est possible.
- Les fichiers de l'application doivent être dans le dossier `/srv/nom-de-application`.

#### Application 3 - Mealie (`feat/mealie`)

Déploie une instance de [Mealie], un gestionnaire de recettes et planificateur de repas. L'application doit s'exécuter 
sur le port `83`. Vous devez déployer l'application avec une base de données **PostgreSQL** (pas *SQLite*).

![Mealie](.docs/mealie.png)

#### Application 4 - Bracket (`feat/bracket`)

Déploie une instance de [Bracket], une application de gestion de tournoi. L'application doit s'exécuter sur le port `84`
et utiliser une base de données PostgreSQL.

![Bracket](.docs/bracket.png)

#### Application 5 - immich (`feat/immich`)

Déploie une instance de [immich], une application pour organiser et gérer ses photos. L'application doit s'exécuter sur 
le port `85`. Cette application possède un conteneur pour analyser les photos avec l'intelligence artificielle : vous
devez utiliser la version *non accélérée*.

> [!NOTE]
> Cette application vous demandera un peu plus d'huile de coude et contient quelques éléments non vus en classe.

![Immich](.docs/immich.png)

### Fusion dans la branche `main`

Fusionne la branche `dev` dans la branche `main`. N'oublie pas de pousser les changements sur GitHub.

## Modalités de remise

Ce travail sera remis sur GitHub Classroom. N'oublie pas de pousser toutes les branches sur GitHub et de vérifier que 
tous tes fichiers ont bien été téléversés. Si tu souhaites remettre le travail en retard, contacte ton professeur par 
MIO, car les travaux seront récupérés le jour exact de la remise.

[Memos]: https://usememos.com/
[Opengist]: https://opengist.io/
[Mealie]: https://docs.mealie.io/
[Bracket]: https://docs.bracketapp.nl/
[immich]: https://immich.app/

