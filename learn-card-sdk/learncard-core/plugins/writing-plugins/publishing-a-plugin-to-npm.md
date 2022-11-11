---
description: Share your work with the world 🌎
---

# Publishing a Plugin to NPM

If you don't have anything secret contained in your plugin, you are encouraged to publish it as a package to NPM and share it with the world 🏆.

Let's walk through how to do that together:

## Make an npm account

If you haven't yet, [follow these short steps to create an npm account](https://docs.npmjs.com/creating-a-new-npm-user-account). You will need to come up with a username, email, and password!

## Create the package boilerplate

As noted in our docs on [The Simplest Plugin](the-simplest-plugin.md#boilerplate), if you've never set up a TS/node package before, we greatly recommend using [aqu](https://www.npmjs.com/package/aqu)!

{% tabs %}
{% tab title="pnpm" %}
<pre class="language-bash"><code class="lang-bash"><strong>yarn dlx aqu create learn-card-example-plugin
</strong>
? Pick package manager: yarn
? Specify package description: () # Describe your plugin!
? Package author: # Who are you?
? Git repository (only for package.json information): 
? Pick license: MIT # See https://choosealicense.com/
<strong>? Pick template: typescript
</strong>
cd learn-card-example-plugin</code></pre>
{% endtab %}

{% tab title="yarn" %}
```bash
pnpm dlx aqu create learn-card-example-plugin

? Pick package manager: pnpm
? Specify package description: () # Describe your plugin!
? Package author: # Who are you?
? Git repository (only for package.json information): 
? Pick license: MIT # See https://choosealicense.com/
? Pick template: typescript

cd learn-card-example-plugin
```
{% endtab %}

{% tab title="npm" %}
```bash
npx aqu create learn-card-example-plugin

? Pick package manager: npm
? Specify package description: () # Describe your plugin!
? Package author: # Who are you?
? Git repository (only for package.json information): 
? Pick license: MIT # See https://choosealicense.com/
? Pick template: typescript

cd learn-card-example-plugin
```
{% endtab %}
{% endtabs %}

## Create a Github Repo

If you've selected an open source license (such as MIT or ISC), please make a Github Repo containing the code to your plugin! If you've never done this before, we recommend using the [Github CLI](https://cli.github.com/).

First, create a [Github Account](https://github.com/join), then install and login with the CLI. This is usually done with the following command:

```bash
gh auth login
```

After getting all setup, initialize and create the repo with the following commands:

```bash
git init

echo "node_modules/" >> .gitignore
echo "dist/" >> .gitignore

git add .
git commit -m "Initial Commit"

gh repo create
? What would you like to do? Push an existing local repository to GitHub
? Path to local repository .
? Repository name learn-card-example-plugin
? Description Example LearnCard Plugin!
? Visibility Public
✓ Created repository {REPOSITORY_NAME} on GitHub
? Add a remote? Yes
? What should the new remote be called? origin
✓ Added remote {REPOSITORY_URL}
? Would you like to push commits from the current branch to "origin"? Yes
✓ Pushed commits to {REPOSITORY_URL}
```

After getting a repo up, it's a good idea to add the URL (shown above as `{REPOSITORY_URL}`) to the `package.json`!

{% code title="package.json" %}
```json
  "repository": {
    "type": "git",
    "url": {REPOSITORY_URL}
  },
```
{% endcode %}

## Release the Package

With everything set up, you may run the release command!

{% tabs %}
{% tab title="pnpm" %}
```bash
pnpm release
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn release
```
{% endtab %}

{% tab title="npm" %}
```bash
npm run release
```


{% endtab %}
{% endtabs %}

If you didn't use aqu to create your package, you may need to use the `publish` command directly:

{% tabs %}
{% tab title="pnpm" %}
```bash
pnpm publish
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn publish
```
{% endtab %}

{% tab title="npm" %}
```bash
npm publish
```
{% endtab %}
{% endtabs %}

Congratulations! 🥳 Your plugin is officially published and others may use it by installing it from npm!
