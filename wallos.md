# Wallos

**Source:** https://github.com/ellite/Wallos

## Overview

This tutorial covers the key resources and tools from the [ellite/Wallos](https://github.com/ellite/Wallos) project.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Demo](#demo)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
    - [Baremetal](#baremetal)
    - [Docker](#docker)
  - [Installation](#installation)
    - [Baremetal](#baremetal-1)
      - [Updating](#updating)
    - [Docker](#docker-1)
    - [Docker-Compose](#docker-compose)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [OIDC](#oidc)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
  - [Contributors](#contributors)
  - [Translations](#translations)
- [License](#license)
- [Links](#links)

## Introduction

Wallos is a powerful, open-source, and self-hostable web application designed to empower you in managing your finances with ease. Say goodbye to complicated spreadsheets and expensive financial software – Wallos simplifies the process of tracking expenses and helps you gain better control over your financial life.

## Features

- Subscription Management: Keep track of your recurring subscriptions and payments, ensuring you never miss a due date.
- Category Management: Organize your expenses into customizable categories, enabling you to gain insights into your spending habits.
- Multi-Currency support: Wallos supports multiple currencies, allowing you to manage your finances in the currency of your choice.
- Currency Conversion: Integrates with the Fixer API so you can get exchange rates and see all your subscriptions on your main currency.
- Data Privacy: As a self-hosted application, Wallos ensures that your financial data remains private and secure on your own server.
- Customization: Tailor Wallos to your needs with customizable categories, currencies, themes and other display options.
- Sorting Options: Allowing you to view your subscriptions from different perspectives.
- Logo Search: Wallos can search the web for the logo of your subscriptions if you don't have them available for upload.
- Mobile view: Wallos on the go.
- Statistics: Another perspective into your spendings.
- Notifications:  Wallos supports multiple notification methods (email, discord, pushover, telegram, gotify and webhooks). Get notified about your upcoming payments.
- Multi Language support.
- OIDC with OAuth
- AI Recommendations with ChatGPT, Gemini or Local Ollama

## Demo

If you want to try Wallos, a demo is available at [https://demo.wallosapp.com](https://demo.wallosapp.com).  
The database is reset every 2 hours.  
To access the demo use the following credentials:

```python
Username: demo  
Password: demo
```

## Getting Started

See instructions to run Wallos below.

## Baremetal

- NGINX or APACHE websever running
- PHP 8.3 with the following modules enabled:
    - curl
    - dom
    - gd
    - imagick
    - intl
    - openssl
    - sqlite3
    - zip
    - mbstring
    - fpm

## Docker

- Docker

## Baremetal

1. Download or clone this repo and move the files into your web root - usually `/var/www/html`
2. Rename `/db/wallos.empty.db` to `/db/wallos.db`
3. Open the app in your browser — migrations run automatically on the registration page
4. Add the following scripts to your cronjobs with `crontab -e`

```bash
0 1 * * * php /var/www/html/endpoints/cronjobs/updatenextpayment.php >> /var/log/cron/updatenextpayment.log 2>&1
0 2 * * * php /var/www/html/endpoints/cronjobs/updateexchange.php >> /var/log/cron/updateexchange.log 2>&1
0 8 * * * php /var/www/html/endpoints/cronjobs/sendcancellationnotifications.php >> /var/log/cron/sendcancellationnotifications.log 2>&1
0 9 * * * php /var/www/html/endpoints/cronjobs/sendnotifications.php >> /var/log/cron/sendnotifications.log 2>&1
*/2 * * * * php /var/www/html/endpoints/cronjobs/sendverificationemails.php >> /var/log/cron/sendverificationemail.log 2>&1
*/2 * * * * php /var/www/html/endpoints/cronjobs/sendresetpasswordemails.php >> /var/log/cron/sendresetpasswordemails.log 2>&1
0 */6 * * * php /var/www/html/endpoints/cronjobs/checkforupdates.php >> /var/log/cron/checkforupdates.log 2>&1
30 1 * * 1 php /var/www/html/endpoints/cronjobs/storetotalyearlycost.php >> /var/log/cron/storetotalyearlycost.log 2>&1
30 3 * * 1 php /var/www/html/endpoints/cronjobs/generaterecommendations.php weekly >> /var/log/cron/generaterecommendations.log 2>&1
0 4 1 * * php /var/www/html/endpoints/cronjobs/generaterecommendations.php monthly >> /var/log/cron/generaterecommendations.log 2>&1
```

5. If your web root is not `/var/www/html/` adjust the cronjobs above accordingly.

## Key Resources

| Resource | Link |
|----------|------|
| https://demo.wallosapp.com | [https://demo.wallosapp.com](https://demo.wallosapp.com) |
| henrique.pt | [https://henrique.pt](https://henrique.pt) |
| wallosapp.com | [https://wallosapp.com](https://wallosapp.com) |
| Discord Server | [https://discord.gg/anex9GUrPW](https://discord.gg/anex9GUrPW) |

