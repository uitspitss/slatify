# Slatify

![GitHub Workflow](https://github.com/homoluctus/slatify/workflows/lint/badge.svg)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/homoluctus/slatify?color=brightgreen)
![GitHub](https://img.shields.io/github/license/homoluctus/slatify?color=brightgreen)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

This is Slack Notification for GitHub Actions.<br>
Generated from [actions/javascript-template](https://github.com/actions/javascript-template).

# ToC

- [Feature](#Feature)
- [Usage](#Usage)
  - [Examples](#Examples)
- [Slack UI](#Slack%20UI)
- [Contribution](#Contribution)
- [LICENSE](#LICENSE)

# Feature
- Notify the result of GitHub Actions
- Support three job status (reference: [job-context](https://help.github.com/en/articles/contexts-and-expression-syntax-for-github-actions#job-context))
  - success
  - failure
  - cancelled
- Mention
  - Notify message to channel members efficiently
  - You can specify the condition to mention

# Usage
First of all, you need to set GitHub secrets for SLACK_WEBHOOK that is Incoming Webhook URL.<br>
You can customize the following parameters:

|with parameter|required/optional|default|description|
|:--:|:--:|:--|:--|
|type|required|N/A|The result of GitHub Actions job<br>This parameter value must contain the following word:<br>- `success`<br>- `failure`<br>- `cancelled`<br>We recommend using ${{ job.status }}|
|job_name|required|N/A|Means slack notification title|
|url|required|N/A|Slack Incoming Webhooks URL<br>Please specify this key or SLACK_WEBHOOK environment variable<br>※SLACK_WEBHOOK will be deprecated|
|mention|optional|N/A|Slack message mention|
|mention_if|optional|N/A|The condition to mention<br>This parameter can contain the following word:<br>- `success`<br>- `failure`<br>- `cancelled`<br>- `always`|
|icon_emoji|optional|Use Slack Incoming Webhook configuration|Slack icon|
|username|optional|Use Slack Incoming Webhook configuration|Slack username|
|channel|optional|Use Slack Incoming Webhook configuration|Slack channel name|
|commit|optional|false|If true, slack notification includes the latest commit message and author.|
|token|case by case|N/A|This token is used to get commit data.<br>If commit parameter is true, this parameter is required.<br>${{ secrets.GITHUB_TOKEN }} is recommended.|

Please refer `action.yml` for more details.

## Examples

```..github/workflows/example1.yml
- name: Slack Notification
  uses: homoluctus/slatify@master
  if: always()
  with:
    type: ${{ job.status }}
    job_name: '*Lint Check*'
    mention: 'here'
    mention_if: 'failure'
    channel: '#random'
    url: ${{ secrets.SLACK_WEBHOOK }}
```

↓ Including the latest commit data

```..github/workflows/example2.yml
- name: Slack Notification
  uses: homoluctus/slatify@master
  if: always()
  with:
    type: ${{ job.status }}
    job_name: '*Lint Check*'
    mention: 'here'
    mention_if: 'failure'
    channel: '#random'
    url: ${{ secrets.SLACK_WEBHOOK }}
    commit: true
    token: ${{ secrets.GITHUB_TOKEN }}
```

<img src="./images/slack2.png" alt="Notification Preview" width="90%">

# Slack UI

<img src="./images/slack.png" alt="Notification Preview" width="90%">

# Contribution

1. Fork this repository
2. Pull your repository in local machine
3. Update original repository
4. Checkout "master" branch based "remotes/origin/master" branch
5. Work on "master" or other branch
6. Push you changes to your repository
7. Create a new Pull Request

# LICENSE

[The MIT License (MIT)](https://github.com/homoluctus/slatify/blob/master/LICENSE)
