---
# NOTE: This file is auto-generated from 'scripts/docgen.mjs'
# Do not make edits to it directly, they will be overwritten.

layout: ~/layouts/MainLayout.astro
title: Référence de configuration
i18nReady: true
setup: |
  import Since from '../../../components/Since.astro';
---

La référence suivante couvre toutes les options de configuration prises en charge dans Astro. Pour en savoir plus sur la configuration d'Astro, lisez notre guide sur la [configuration d'Astro](/fr/guides/configuring-astro/).

```js
// astro.config.mjs
import { defineConfig } from 'astro/config'

export default defineConfig({
  // Vos options de configuration ici...
})
```
## Options de niveau supérieur

### root

<p>

**Type:** `string`<br>
**CLI:** `--root`<br>
**Par défaut:** `"."` (répertoire de travail actuel)
</p>

Vous ne devez fournir cette option que si vous exécutez la commande CLI `astro` dans un répertoire autre que le répertoire racine du projet. Habituellement, cette option est fournie via le CLI au lieu du [fichier de configuration Astro](/fr/guides/configuring-astro/#types-de-fichier-de-configuration-supportés), car Astro doit connaître la racine de votre projet avant de pouvoir localiser votre fichier de configuration.

Si vous fournissez un chemin relatif (ex: `--root: './my-project'`) Astro va le résoudre par rapport à votre répertoire de travail actuel.

#### Exemples

```js
{
  root: './my-project-directory'
}
```
```bash
$ astro build --root ./my-project-directory
```


### srcDir

<p>

**Type:** `string`<br>
**Par défaut:** `"./src"`
</p>

Définissez le répertoire à partir duquel Astro lira votre site.

La valeur peut être soit un chemin absolu du système de fichiers, soit un chemin relatif à la racine du projet.

```js
{
  srcDir: './www'
}
```


### publicDir

<p>

**Type:** `string`<br>
**Par défaut:** `"./public"`
</p>

Définissez le répertoire de vos ressources statiques. Les fichiers de ce répertoire sont servis à `/` pendant le développement et copiés dans votre répertoire de build pendant la phase de build. Ces fichiers sont toujours servis ou copiés tels quels, sans transformation ni regroupement.

La valeur peut être soit un chemin absolu du système de fichiers, soit un chemin relatif à la racine du projet.

```js
{
  publicDir: './my-custom-publicDir-directory'
}
```


### outDir

<p>

**Type:** `string`<br>
**Par défaut:** `"./dist"`
</p>

Définissez le répertoire dans lequel `astro build` écrit votre version finale.

La valeur peut être soit un chemin absolu du système de fichiers, soit un chemin relatif à la racine du projet.

```js
{
  outDir: './my-custom-build-directory'
}
```


### site

<p>

**Type:** `string`
</p>

Votre URL finale déployée. Astro utilise cette URL complète pour générer votre sitemap et vos URL canoniques dans votre version finale. Il est fortement recommandé de définir cette configuration pour tirer le meilleur parti d'Astro.

```js
{
  site: 'https://www.my-site.dev'
}
```


### base

<p>

**Type:** `string`
</p>

Le chemin de base vers lequel vous effectuez le déploiement. Astro correspondra à ce nom de chemin d'accès pendant le développement afin que votre expérience de développement corresponde la plus possible à votre environnement de build. Dans l'exemple c-dessous, `astro dev` démarrera votre serveur à `/docs`.

```js
{
  base: '/docs'
}
```


### trailingSlash

<p>

**Type:** `'always' | 'never' | 'ignore'`<br>
**Par défaut:** `'ignore'`
</p>

Définissez la route correspondante au comportement du serveur dev. Choisissez parmi les options suivantes :
  - `'always'` - Ne correspond qu'aux URL qui incluent un slash de fin (ex: "/foo/")
  - `'never'` - Ne correspond à aucune URL incluant un slash de fin (ex: "/foo")
  - `'ignore'` - Correspond aux URL qu'il existe ou non un "/" à la fin.

Utilisez cette option de configuration si votre hôte de production a une gestion stricte du fonctionnement ou du non-fonctionnement des slashs finaux.

Vous pouvez également le définir si vous préférez être vous-même plus strict, afin que les URL avec ou sans slash à la fin ne fonctionnent pas pendant le développement.

```js
{
  // Exemple: Exiger un slash final pendant le développement
  trailingSlash: 'always'
}
```
**Voir également :**
- buildOptions.format


### adapter

<p>

**Type:** `AstroIntegration`
</p>

Déployez-le sur votre serveur préféré, sans serveur ou hôte périphérique avec des adaptateurs de build. Importez l'un de nos adaptateurs pour [Netlify](/fr/guides/deploy/netlify/#adapter-for-ssredge), [Vercel](/fr/guides/deploy/vercel/#adapter-for-ssr), et plus encore pour activer Astro SSR.

[Voir notre guide de rendu côté serveur](/fr/guides/server-side-rendering/) pour en savoir plus sur le SSR, et [nos guides de déploiement](/fr/guides/deploy/) pour une liste complète d'hôtes.

```js
import netlify from '@astrojs/netlify/functions';
{
  // Exemple: Construire pour un déploiement sans serveur Netlify
	 adapter: netlify(),
}
```
**Voir également :**
- output


### output

<p>

**Type:** `'static' | 'server'`<br>
**Par défaut:** `'static'`
</p>

Spécifie la cible de sortie pour les builds.

- 'static' - Construire un site statique à déployer sur n’importe quel hôte statique.
- 'server' - Création d’une application à déployer sur un hôte prenant en charge le SSR (rendu côté serveur).

```js
import { defineConfig } from 'astro/config';

export default defineConfig({
  output: 'static'
})
```
**Voir également :**
- adapter


## Options de build

### build.format

<p>

**Type:** `('file' | 'directory')`<br>
**Par défaut :** `'directory'`
</p>

Contrôlez le format de fichier de sortie de chaque page.
  - Si la valeur est 'file', Astro générera un fichier HTML (ex: "/foo.html") pour chaque page.
  - Si la valeur est 'directory', Astro générera un répertoire avec un fichier imbriqué `index.html` (ex: "/foo/index.html") pour chaque page.

```js
{
  build: {
    // Exemple: Générer `page.html` au lieu de `page/index.html` durant le build.
    format: 'file'
  }
}
```

#### Effets sur Astro.url
Le paramètre `build.format` contrôle ce à quoi `Astro.url` est défini pendant la compilation. Quand il est défini sur:
- `directory` - L'`Astro.url.pathname` inclura un slash pour imiter le comportement des dossiers; c.-à-d. `/foo/`.
- `file` - L'`Astro.url.pathname` inclura `.html`; c.-à-d. `/foo.html`.

Cela signifie que lorsque vous créez des URL relatives en utilisant `new URL('./relative', Astro.url)`, vous obtiendrez un comportement cohérent entre dev et build.


## Options de serveur

Personnalisez le serveur Astro dev, utilisé par `astro dev` et `astro preview`.

```js
{
  server: { port: 1234, host: true }
}
```

Pour définir une configuration différente basée sur la commande run ("dev", "preview") une fonction peut également être passée à cette option de configuration.

```js
{
  // Exemple: Utiliser la syntaxe de fonction pour personnaliser le serveur en fonction de la commande
  server: (command) => ({ port: command === 'dev' ? 3000 : 4000 })
}
```

### server.host

<p>

**Type:** `string | boolean`<br>
**Par défaut:** `false`<br>
<Since v="0.24.0" />
</p>

Définir les adresses IP réseau sur lesquelles le serveur doit écouter (c.-à-d. les adresses IP non locales).
- `false` - ne pas exposer sur une adresse IP réseau
- `true` - écouter toutes les adresses, y compris les adresses LAN et publiques
- `[custom-address]` - exposer sur une adresse IP réseau à `[custom-address]` (ex: `192.168.0.1`)


### server.port

<p>

**Type:** `number`<br>
**Par défaut:** `3000`
</p>

Définissez le port sur lequel le serveur doit écouter.

Si le port donné est déjà utilisé, Astro va automatiquement essayer le prochain port disponible.

```js
{
  server: { port: 8080 }
}
```


## Options de Markdown

### markdown.drafts

<p>

**Type:** `boolean`<br>
**Par défaut:** `false`
</p>

Contrôler si les pages de projet Markdown doivent être incluses dans la construction.

Une page Markdown est considérée comme un brouillon si elle inclut `draft: true` dans son avant-propos. Les brouillons de pages sont toujours inclus et visibles pendant le développement (`astro dev`) mais par défaut, ils ne seront pas inclus dans votre build final.

```js
{
  markdown: {
    // Exemple: Inclure tous les brouillons dans votre version finale
    drafts: true,
  }
}
```


### markdown.shikiConfig

<p>

**Type:** `Partial<ShikiConfig>`
</p>

Options de configuration Shiki. Voir [la documentation de configuration Markdown](/fr/guides/markdown-content/#configuration-de-shiki) pour l'utilisation.


### markdown.syntaxHighlight

<p>

**Type:** `'shiki' | 'prism' | false`<br>
**Défaut:** `shiki`
</p>

Quel surligneur de syntaxe utiliser, le cas échéant.
- `shiki` - utiliser le surligneur [Shiki](https://github.com/shikijs/shiki)
- `prism` - utiliser le surligneur [Prism](https://prismjs.com/)
- `false` - ne pas appliquer la mise en évidence de la syntaxe.

```js
{
  markdown: {
    // Exemple: Passer à l’utilisation de prism pour la mise en évidence de la syntaxe dans Markdown
    syntaxHighlight: 'prism',
  }
}
```


### markdown.remarkPlugins

<p>

**Type:** `RemarkPlugins`
</p>

Passer un [plugin remark](https://github.com/remarkjs/remark) pour personnaliser la façon dont votre Markdown est construit. Vous pouvez importer et appliquer la fonction du plugin (recommandé), ou passer le nom du plugin comme une chaîne de caractère.

:::caution
Fournir une liste de plugins va **supprimer** nos plugins par défaut. Pour préserver ces valeurs par défaut, voir le drapeau `extendDefaultPlugins`.
:::

```js
{
  markdown: {
    remarkPlugins: [remarkToc]
  }
}
```


### markdown.rehypePlugins

<p>

**Type:** `RehypePlugins`
</p>

Passez un [plugin rehype](https://github.com/remarkjs/remark-rehype) pour personnaliser la manière dont le résultat HTML de sortie de votre Markdown sera traité. Vous pouvez importer et appliquer la fonction du plugin (recommandé), ou juste pass le nom du plugin en tant que chaine de caractères.

:::caution
Fournir une liste de plugins va **retirer** nos plugins par défaut. Pour les préserver, regardez l'option `extendDefaultPlugins`.
:::

```js
import rehypeMinifyHtml from 'rehype-minify';
{
  markdown: {
    rehypePlugins: [rehypeMinifyHtml]
  }
}
```


### markdown.extendDefaultPlugins

<p>

**Type :** `boolean`<br>
**Par défaut :** `false`
</p>

Astro applique par défaut les plugins [Markdown de GitHub](https://github.com/remarkjs/remark-gfm) et [Smartypants](https://github.com/silvenon/remark-smartypants). Quand vous ajoutez votre propre plugin remark ou rehype, vous pouvez préserver ces plugins par défaut en paramétrant l'option `extendDefaultPlugins` sur `true` 

```js
{
  markdown: {
    extendDefaultPlugins: true,
		 remarkPlugins: [exampleRemarkPlugin],
    rehypePlugins: [exampleRehypePlugin],
  }
}
```


### markdown.remarkRehype

<p>

**Type:** `RemarkRehype`
</p>

Passez les options à [remark-rehype](https://github.com/remarkjs/remark-rehype#api).

```js
{
  markdown: {
    // Exemple: Traduire le texte du footer dans un autre langage, ce sont les valeurs anglaises par défaut.
    remarkRehype: { footnoteLabel: "Footnotes", footnoteBackLabel: "Back to content"},
  },
};
```


## Intégrations

Étendez Astro avec des intégrations personnalisées. Les intégrations sont votre guichet unique pour ajouter la prise en charge du framework (comme Solid.js), de nouvelles fonctionnalités (comme les sitemaps) et de nouvelles bibliothèques (comme Partytown et Turbolinks).

Lisez notre [Guide d'intégration](/fr/guides/integrations-guide/) pour vous aider à débuter avec les intégrations Astro.

```js
import react from '@astrojs/react';
import tailwind from '@astrojs/tailwind';
{
  // Exemple: Ajouter la prise en charge de React + Tailwind par Astro
  integrations: [react(), tailwind()]
}
```

## Vite

Passez des options de configuration supplémentaires à Vite. Utile lorsque Astro ne prend pas en charge certaines configurations avancées dont vous pourriez avoir besoin.

Regardez la documentation complète de l'objet de configuration de `vite` sur [vitejs.dev](https://vitejs.dev/config/).

#### Exemples

```js
{
  vite: {
    ssr: {
      // Exemple: Forcer un package cassé à passer outre le processus SSR si besoin.
      external: ['broken-npm-package'],
    }
  }
}
```

```js
{
  vite: {
    // Exemple: Ajout des plugins personnalisés vite directement à votre projet Astro.
    plugins: [myPlugin()],
  }
}
```

## Options héritées

Pour aider certains utilisateurs à migrer entre les versions d’Astro, nous introduisons occasionnellement des options `héritées`.
Ces options vous permettent d’opter pour un comportement déprécié ou autrement dépassé d'Astro
dans la dernière version, afin que vous puissiez continuer à mettre à jour et profiter des nouvelles versions d’Astro.

### legacy.astroFlavoredMarkdown

<p>

**Type:** `boolean`<br>
**Par défaut:** `false`<br>
<Since v="1.0.0-rc.1" />
</p>

Activer le support de la pre-v1.0 Astro pour les composants et expressions JSX dans les fichiers Markdown `.md`.
Dans Astro `1.0.0-rc`, ce comportement original a été supprimé par défaut, en faveur de notre nouvelle [intégration MDX](/fr/guides/integrations-guide/mdx/).

Pour activer ce comportement, définissez `legacy.astroFlavoredMarkdown` sur `true` dans votre [fichier de configuration `astro.config.mjs`](/fr/guides/configuring-astro/#le-fichier-de-configuration-dastro).

```js
{
  legacy: {
    // Exemple: Ajout de la prise en charge des anciennes fonctionnalités Markdown
    astroFlavoredMarkdown: true,
  },
}
```
