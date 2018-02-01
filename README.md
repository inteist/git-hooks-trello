<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [About](#about)
- [Versions](#versions)
    - [1.0](#10)
- [Installation How-To](#installation-how-to)
  - [Environment config](#environment-config)
  - [Script Config](#script-config)
  - [Get card IDs to show in Trello](#get-card-ids-to-show-in-trello)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<p align="center">
<img src="https://github.com/inteist/git-hooks-trello/blob/master/trello-git-hooks-logo.png">
</p>

# About

This is a full suit of tools to be able to enable git hooks to interface with Trello


# Versions

### 1.0
- add comments with associated git commit and alternatively close/archive issues from git commits


# Installation How-To


## Environment config

- Install node
- Install `node_trello` and `colors` packages globally

```bash
sudo npm install -g node-trello
```

```bash
sudo npm install -g colors
```
- Clone this repo
- make symlink to `post-commit` and `post-to-trello`

```bash
ln -s /link/to/your/post-commit .git/hooks/post-commit
ln -s /link/to/your/post-to-trello .git/hooks/post-to-trello
```
- Make the hooks executable

```bash
chmod +x .git/hooks/*
```

- run `git init` to reinitialize the repository to make sure it picks the new hooks



## Script Config

- **STEP 1** - get an app key:

`https://trello.com/1/appKey/generate`


- **STEP 2** - get an app token using app key from step 1

`https://trello.com/1/connect?key=<KEY_FROM_STEP_1>&name=git-hook&expiration=never&response_type=token&scope=read,write`

(replace KEY_FROM_STEP_1 with an actual key you got in STEP 1)

- **STEP 3** - get board ID:

append `.json` to any URL while inside the board and look for `id: "BOARD_ID",`

find completed board id this way as well.

- **STEP 4** replace

`key`, `token` and `board_id` `completed_board_id` with the values obtained in steps 1-3

Set environment variables.

```
export TRELLO_KEY="key"
export TRELLO_TOKEN="token"
export BOARD_ID="board ID"
export REPO_LINK="link to your repostiory"
export COMPLETED_LIST_ID="completed board id"
```



## Get card IDs to show in Trello

Use this bookmarklet:

```js
javascript:!function(){var o=$(".card-short-id");o.each(function(){$(this).text($(this).text().replace("","").replace("","").replace("N.º ", ""))});o.hasClass("hide")?o.removeClass("hide").css({"font-weight":"normal","font-size":".9em","margin-right":"5px",padding:"2.3px 6px",background:$("body").css("background-color"),"border-radius":"10px",color:"#EE433E"}):o.addClass("hide")}();

```

Note that due to how Trello injects newly added cards, this won't work on newly added cards unless you refresh the page and toggle this bookmarklet again
