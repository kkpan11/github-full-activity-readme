# GitHub Activity in Readme

Updates `README.md` with the recent GitHub activity of a user.

Here's [my](https://github.com/Pop101/Pop101) recent commits:
<!--START_SECTION:activity-->
1. 🍴 Forked [recent-activity](https://github.com/Readme-Workflows/recent-activity) to [recent-activity](https://github.com/kkpan11/recent-activity)
2. ⭐️ Starred [recent-activity](https://github.com/Readme-Workflows/recent-activity)
3. 📦 Pushed 2 commits to [github-full-activity-readme](https://github.com/kkpan11/github-full-activity-readme)
4. ⭐️ Starred [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)
5. ⭐️ Starred [prettier-eslint](https://github.com/prettier/prettier-eslint)
<!--END_SECTION:activity-->

---

## Instructions

- Add the comment `<!--START_SECTION:activity-->` (entry point) within `README.md`. You can find an example [here](https://github.com/Pop101/Pop101/blob/master/README.md).

- It's the time to create a workflow file.

`.github/workflows/update-readme.yml`

```yml
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    name: Update this repo's README with recent activity

    steps:
      - uses: actions/checkout@v2
      - uses: Pop101/github-full-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

The above job runs every half an hour, you can change it as you wish based on the [cron syntax](https://jasonet.co/posts/scheduled-actions/#the-cron-syntax).

Most public events show up, including

- Commenting on Issues
- Opening and Closing Issues
- Opening Pull Requests
- Pushing to Repositories
- Forking Repositories
- Starring Repositories
- Repositories Creation and Publishing

### Override defaults

Use the following `input params` to customize it for your use case:-

| Input Param | Default Value | Description |
|--------|--------|--------|
| `COMMIT_MSG` | ":zap: Update README with the recent activity" | Commit message used while committing to the repo |
| `MAX_LINES` | 5 | The maximum number of lines populated in your readme file |
| `EVENT_TYPES` | "IssueCommentEvent,IssuesEvent,PullRequestEvent,PushEvent,ForkEvent,WatchEvent,PublicEvent,CreateEvent" | The event types to be included in the readme file. You can find the list of event types [here](https://docs.github.com/en/free-pro-team@latest/developers/webhooks-and-events/github-event-types) |

```yml
name: Update README

on:
  schedule:
    - cron: '*/30 * * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    name: Update this repo's README with recent activity

    steps:
      - uses: actions/checkout@v2
      - uses: Pop101/github-full-activity-readme@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          COMMIT_MSG: 'Specify a custom commit message'
          MAX_LINES: 10
          EVENT_TYPES: 'PushEvent,WatchEvent'
```

