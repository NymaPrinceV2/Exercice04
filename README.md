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