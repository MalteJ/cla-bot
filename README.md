# cla-bot

cla-bot is a GitHub Application for automation of Contributor Licence Agreements (CLAs). It checks whether contributors have signed an agreement, adding labels to PRs if they have, or prompting for signature if they have not.

This bot has the following features:
 - Easily integrates with projects or entire organisations via a GitHub App
 - Automatically checks every pull request and every commit
 - Pull requests are re-checked on each push
 - The approved contributor list can be maintained in various ways including JSON files or a webhook
 - A re-check for a pull request can be triggered via a comment
 - Uses labels and status checks to make the process visible
 - Provides a fully-hosted solution, you don't have to maintain your own bot installation
 - You can provide templates for the various messages this bot posts

## Used by ...

This bot checks over 20,000 PRs each month and is used by a number of prominent open source projects including:

<table>
<tr>
  <td>
    <a href="https://www.nativescript.org/"><img src="https://avatars3.githubusercontent.com/u/7392261?s=50"/>
    <br/>NativeScript</a>
  </td>
  <td>
    <a href="https://trino.io/"><img src="https://avatars2.githubusercontent.com/u/34147222?s=50"/>
    <br/>Trino</a>
  </td>
  <td>
    <a href="https://www.demandware.com/"><img src="https://avatars3.githubusercontent.com/u/1315434?s=50"/>
    <br/>Salesforce</a>
  </td>
  <td>
    <a href="https://github.com/Seagate"><img src="https://avatars2.githubusercontent.com/u/5016309?s=50"/>
    <br/>Seagate</a>
  </td>
  <td>
    <a href="https://mailchimp.com/"><img src="https://avatars2.githubusercontent.com/u/216758?s=50"/>
    <br/>Mailchimp</a>
  </td>
  <td>
    <a href="https://web3.foundation/"><img src="https://avatars0.githubusercontent.com/u/30405397?s=50"/>
    <br/>Web3</a>
  </td>
  <td>
    <a href="https://www.mautic.org/"><img src="https://avatars2.githubusercontent.com/u/5257677?s=50"/>
    <br/>Mautic</a>
  </td>
</tr>
<tr>
  <td>
    <a href="https://www.codecademy.com/"><img src="https://avatars3.githubusercontent.com/u/1463944?s=50"/>
    <br/>Codecademy</a>
  </td>
  <td>
    <a href="https://conda.io/"><img src="https://avatars2.githubusercontent.com/u/6392739?s=50"/>
    <br/>Conda</a>
  </td>
  <td>
    <a href="http://v2.onivim.io/"><img src="https://avatars0.githubusercontent.com/u/31161891?s=50"/>
    <br/>onivim</a>
  </td>
  <td>
    <a href="http://egghead.io/"><img src="https://avatars2.githubusercontent.com/u/5975001?s=50"/>
    <br/>Egghead</a>
  </td>
  <td>
    <a href="http://geonode.org/"><img src="https://avatars0.githubusercontent.com/u/132843?s=50"/>
    <br/>GeoNode</a>
  </td>
  <td>
    <a href="https://www.graycore.io/"><img src="https://avatars3.githubusercontent.com/u/33813698?s=50"/>
    <br/>Graycore</a>
  </td>
  <td>
    <a href="http://www.hivemq.com/"><img src="https://avatars1.githubusercontent.com/u/4578332?s=50"/>
    <br/>HiveMQ</a>
  </td>
</tr>
<tr>
  <td>
    <a href="https://gauge.org/"><img src="https://avatars0.githubusercontent.com/u/7044589?s=50"/>
    <br/>Gauge</a>
  </td>
  <td>
    <a href="https://finos.org/"><img src="https://avatars0.githubusercontent.com/u/35377814?s=50"/>
    <br/>FINOS</a>
  </td>
  <td>
    <a href="https://www.predix-ui.com/#/home"><img src="https://avatars0.githubusercontent.com/u/32078779?s=50"/>
    <br/>Predix</a>
  </td>
  <td>
    <a href="https://www.devcolor.org/"><img src="https://avatars0.githubusercontent.com/u/17156358?s=50"/>
    <br/>dev/color</a>
  </td>
  <td>
    <a href="http://gladius.io/"><img src="https://avatars0.githubusercontent.com/u/32402535?s=50"/>
    <br/>Gladius</a>
  </td>
  <td>
    <a href="https://storj.io/"><img src="https://avatars0.githubusercontent.com/u/6308081?s=50"/>
    <br/>Storj</a>
  </td>
  <td>
    <a href="https://www.skylight.io/"><img src="https://avatars0.githubusercontent.com/u/4999088?s=50"/>
    <br/>Skylight</a>
  </td>
</tr>
</table>

## What is a CLA?

If you maintain an open source project you'll likely have selected an open source licence that governs your project. This provides an implicit agreement for contributors to your project, whereas a Contributor Licence Agreement (CLA) makes these terms explicit and provides a record of these agreements.

As described via [Wikipedia](https://en.wikipedia.org/wiki/Contributor_License_Agreement)

> The purpose of a CLA is to ensure that the guardian of a project's outputs has the necessary ownership or grants of rights over all contributions to allow them to distribute under the chosen license.

You can find example CLAs from [GitHub](https://cla.github.com/), [Facebook](https://code.facebook.com/cla), [Microsoft](https://cla.microsoft.com/), [JSFoundation](https://js.foundation/CLA) and many other projects.

## What does cla-bot do?

Adding a CLA to your project workflow can add quite a bit of overhead. For each pull request you need to ensure that each committer has signed your CLA before merging. For small projects this can probably be done manually, but for larger projects you probably want to automate this process.

As you can see from the above examples CLAs differ between projects, and the mechanics for signing them also differ. For that reason this bot doesn't automate that part of the process. However, the process of checking pull requests against a list of (approved) contributors is what this bot automates.

For projects that use the cla-bot, when a pull request is opened, the commits are checked to determine the CLA status for each committer. If any fail the check, the bot posts a (customisable) comment, prompting them to get in touch and arrange a CLA:

![cla bot comment](screenshots/bot-comment.png)

If the checks pass, a (configurable) label is added to the pull request:

![cla bot label](screenshots/bot-label.png)

In each case the pull request status is set to a pass or fail. It's a good idea to make the `verification/cla-signed` status a required status check so that it must pass before pull requests are merged.

If a committer signs the CLA and you wish to have a pull request re-check, you can request this posting a comment that contains the text `@cla-bot check`:

![cla bot label](screenshots/bot-recheck.png)

## Installing cla-bot

The cla-bot is a GitHub App making it very easy to install for individual projects, or entire organizations. You don't have to host anything yourself in order to run the bot, you simply provide configuration. To install the bot, visit [https://github.com/apps/cla-bot](https://github.com/apps/cla-bot), click 'Install', and select the project(s) that you want to enable cla-bot on. Once enabled, cla-bot will be informed whenever a pull request is opened or updated on any of the selected repositories.

When a pull request is opened, cla-bot checks all the committers to ensure that they have a signed CLA. In order for cla-bot to perform this check you need to add a `.clabot` file to your repository. There are various configuration options available for specifying how contributors are verified, with the most simple being a list of GitHub accounts for contributors with a CLA.

You might want to try out the bot in a test repo. Here's an example `.clabot` file:

~~~json
{
  "contributors": ["YourUsername"]
}
~~~

Once added, try creating a pull request to see the bot in action.

All of the configuration relating to this bot is performed via the `.clabot` file.

## Configuration options

### .clabot resolution

The `.clabot` is automatically resolved in the root project folder (for example this project resolves the following file, `https://github.com/ColinEberhardt/cla-bot/.clabot`).

If you have multiple repositories within the same organization, or user account, that have the same contributors, you can create a single configuration by adding a project called `clabot-config`. For example, for my personal projects I could configure the bot via `https://github.com/ColinEberhardt/clabot-config/.clabot`. Also make sure to give the "cla-bot Github App" access rights to `clabot-config` repository. You can do this either when installing the "cla-bot Github App" or later by visiting [https://github.com/apps/cla-bot](https://github.com/apps/cla-bot).

Note, if you do not want the list of contributors to be public, the `clabot-config` project can be private.

### configuration schema

The `.clabot` file has four properties:

~~~json
{
  "contributors": "...",
  "message": "...",
  "label": "...",
  "recheckComment": "..."
}
~~~

 - `contributors` - details the contributors with signed CLAs, more on this later.
 - `message` (optional) - the message that the bot adds as a comment if an of the committers for a pull request have not signed a CLA.
 - `label` (optional) - the label applied to a pull request if all committers have a signed CLA.
 - `recheckComment` (optional) - the comment added when the bot is manually requested to re-check a pull request.

### contributors option

There are various ways in which you can specify the list of contributors:

You can embed the contributors directly into the `.clabot` file as an array of GitHub usernames:

~~~json
{
  "contributors": [ "frank", "bob", "sam" ]
}
~~~

You can specify a URL which returns the contributors list (as a JSON array)

~~~json
{
  "contributors": "http://foo.com/static/contributors"
}
~~~

If the contributors URL uses the GitHub API, the bot will be authenticated, allowing it to access private repositories

~~~json
{
  "contributors": "https://api.github.com/repos/foo/bar/contents/.contributors"
}
~~~

You can supply a webhook which has a querystring that is invoked for each committer:

~~~json
{
  "contributors": "http://foo.com/contributor?checkContributor="
}
~~~

With each invocation, the `checkContributor` querystring parameter is used to supply the committer username. The webhook should return a JSON response that indicates whether the committer has signed a CLA:

~~~json
{
  "isContributor": true
}
~~~

### Adding a custom message

If you wish to add a custom message, include a `message` property within the `.cla-bot` file. This can optionally include a `{% raw %}{{usersWithoutCLA}}{% endraw %}` token which is expanded out to the names of the contributors who have not signed a CLA.

For example:

~~~json
{
  "message": "We require contributors to sign our Contributor License Agreement, and we don\"t have {{usersWithoutCLA}} on file. In order for us to review and merge your code, please contact @FriendlyAdmin to get yourself added."
}
~~~

It is good practice to include details of who to contact in order to go ahead with the CLA signing process.

### Adding a custom label

If a PR is opened where all the contributors have signed the CLA, it is labelled with `cla-signed`. You can configure this behaviour as follows:

~~~json
{
  "label": "my-custom-label"
}
~~~

## Privacy Policy

Your privacy is important to us. It is cla-bot's policy to respect your privacy regarding any information we may via the GitHub app integration. This bot does not collect or store any personal information.

The process of verifying a contributors CLA generates a log file which is publicly available, and accessible via the associated pull request status. These log files are retained indefinitely as they are an integral part of the bot's function. If you have any concerns, or spot any privacy related issues with these files, please raise an issue and these will be addressed as a priority.

## Development

You know ... the usual ...

~~~console
npm install
~~~

### Running locally

For most end users cla-bot will be added to a project as an integration, this provides the simplest integration experience. However, this is also the most complex from a set-up perspective! In order to simplify things, in development, you can run the bot as a simple webhook integration.

1. Create a [personal access token](https://github.com/settings/tokens) for the account that you want to run the bot as.
2. Edit `dev/.env.example`, renaming to `dev/.env`, and add the personal access token generated above to `GITHUB_ACCESS_TOKEN`.
3. Ensure `INTEGRATION_ENABLED` is set to false.
4. Find a suitable repo to test against, and add a `.clabot` file.
5. The `dev/event.json` provides an example webhook (with most of the fields removed) that the bot receives when a PR is opened. Edit this file so that it points to a PR in your test repository.
6. The bot comments, adds labels, and updates the status of commits. In order to do this it needs write access to the repo. Note that the integration only requests the minimal permissions required to perform these functions. Either the repo you are using to test against in (4) needs to be owned by the user from (1), or you need to add the user as a collaborator or team member.
7. You're ready to go!!!

Run the bot as follows:

```
$ npm run execute  
```


