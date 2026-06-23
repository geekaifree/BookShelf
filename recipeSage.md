# RecipeSage Self-Hosting Toolkit

**Source:** https://github.com/julianpoy/RecipeSage-selfhost

## Overview

This tutorial covers the key resources and tools from the [julianpoy/RecipeSage-selfhost](https://github.com/julianpoy/RecipeSage-selfhost) project.

## RecipeSage Self-Hosting Toolkit

[RecipeSage](https://recipesage.com) is a free personal recipe keeper, meal planner, and shopping list organizer for Web, IOS, and Android. It can be used to share recipes, shopping lists, and meal plans with your family & friends, as well as import (grab) recipes from any URL on the web.

This repository contains the configuration needed to run your own, personal instance of [RecipeSage](https://recipesage.com).

The docker images used here are based on the same version that the official [RecipeSage](https://recipesage.com) uses in the cloud for the hosted instance. I'm mostly focused on the official hosted instance, but please let me know if there are issues when attempting to run it locally!

## License/Usage Restrictions

Please note that this repository and all public RecipeSage branding, docker images, code, binaries, and everything else are for personal, private (non-public), non commercial use only. All RecipeSage branding is not licensed for reuse.

Warning: There are portions of the software that may not work. I don't warranty the functionality here. You're in charge of making backups and making sure you don't lose data, especially when updating!

## Setup

For Synology boxes, see [this setup guide instead](./SETUP-SYNOLOGY.md).

1. You'll need Docker to run [RecipeSage](https://recipesage.com) locally. Although you _can_ attempt to run it without Docker, you're on your own.
2. Start all containers with `docker compose up -d`
3. The app should be available at port 7270. You can change that by changing [this](https://github.com/julianpoy/RecipeSage-selfhost/blob/a1133c51af24ca78f9bc9537e147411b5e7e311a/docker-compose.yml#L8) to something else, such as `3000:80` for port 3000.

You'll very likely want to put RecipeSage behind a reverse proxy for SSL termination (and so that you can run more than just RecipeSage!). That's not covered by this README, but I encourage you look at [Caddy](https://caddyserver.com/docs/install) or [Nginx Proxy Manager](https://nginxproxymanager.com/guide) if you are unfamiliar with reverse proxies. A reverse proxy isn't strictly necessary to use RecipeSage self-hosted, however.

## Updating

By default, the database will be automatically migrated when updating to a new container version. As with any migration/upgrade, I **strongly recommend taking a backup** of your volumes before migrating to avoid any potential data loss. My first recommendation when encountering issues after an update will be to rollback, which will be impossible if you don't have a backup.

1. [_Take a look at the changelog below for any special upgrade notes_](#changelog). Then follow the steps below.

2. Update your local copy of this repo with the latest from this repository. If cloned with Git, this is as simple as `git pull`.

3. Update your local images: `docker compose pull`.

4. Down & up the containers: `docker compose down --remove-orphans && docker compose up -d`

## Customization

The following sections provide some information on customizing your instance. Following the "setup" section is enough to get you running with a RecipeSage instance like that of the official site.

## Disabling Registration

If you want to disable registration, **after** you have registered yourself as a user, add this to the top of the docker environment variables: 
`DISABLE_REGISTRATION=true` 

Then, down & up the containers: `docker compose down && docker compose up -d`

When registration is disabled, the registration screen will still appear but will fail with an error if anyone tries to register.

## Bonus Features

The "bonus features" from the hosted version can be activated by running the following command (swap out the email address with your account email).
Please contribute to the development & maintenance of RecipeSage at https://recipesage.com/#/contribute -- Julian.

`./activate.sh example@example.com`

## OpenAI API Keys

_This section is optional, but does enable some features_

Some of the features within the app rely on an OpenAI API key and will not be functional by default. This includes the "scan from image", "scan from PDF", and "autofill from text" features. Additionally, OpenAI provides a fallback in the case that the recipe clipper is unable to find a match.

**I cannot provide support for setting up an OpenAI account.**

1. Create an API key with OpenAI at [https://platform.openai.com](https://platform.openai.com) and setup your credit card with them
2. Set `OPENAI_API_KEY` in your docker-compose to the API key you created (it's already in there, just with no value)
3. Re-create the containers via docker-compose if you've already started them

## Using an OpenAI alternative

You can use an OpenAI alternative by adding a new environment variable to your API container.

The `OPENAI_API_BASE_URL` should be set to an OpenAI-compatible endpoint. See the OpenAI documentation for this -- _please_ do not open issues related to non-OpenAI API support -- I do not provide support for this, and only pass the environment variable straight through directly to OpenAI's library.

## Key Resources

| Resource | Link |
|----------|------|
| RecipeSage | [https://recipesage.com](https://recipesage.com) |
| RecipeSage | [https://recipesage.com](https://recipesage.com) |
| RecipeSage | [https://recipesage.com](https://recipesage.com) |
| RecipeSage | [https://recipesage.com](https://recipesage.com) |
| this | [https://github.com/julianpoy/RecipeSage-selfhost/blob/a1133c51af24ca78f9bc9537e147411b5e7e311a/docker-compose.yml#L8](https://github.com/julianpoy/RecipeSage-selfhost/blob/a1133c51af24ca78f9bc9537e147411b5e7e311a/docker-compose.yml#L8) |
| Caddy | [https://caddyserver.com/docs/install](https://caddyserver.com/docs/install) |
| Nginx Proxy Manager | [https://nginxproxymanager.com/guide](https://nginxproxymanager.com/guide) |
| https://platform.openai.com | [https://platform.openai.com](https://platform.openai.com) |
| old Dockerfile | [https://github.com/julianpoy/RecipeSage-selfhost/blob/13dd943fb1c9a9d0d74cb1af21ef40bd585e2033/docker-compose.yml#L100-L108](https://github.com/julianpoy/RecipeSage-selfhost/blob/13dd943fb1c9a9d0d74cb1af21ef40bd585e2033/docker-compose.yml#L100-L108) |
| volume definition | [https://github.com/julianpoy/RecipeSage-selfhost/blob/main/docker-compose.yml#L126-L127](https://github.com/julianpoy/RecipeSage-selfhost/blob/main/docker-compose.yml#L126-L127) |

