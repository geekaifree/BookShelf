# Wingfit

**Source:** https://github.com/itskovacs/wingfit

## Overview

This tutorial covers the key resources and tools from the [itskovacs/wingfit](https://github.com/itskovacs/wingfit) project.

## 📝 Table of Contents

- 📦 [About](#about)
- 🌱 [Getting Started](#getting_started)
- 📸 [Demo](#Demo)
- 🚧 [Roadmap](#Roadmap)
- 📜 [License](#License)
- 🤝 [Contributing](#Contributing)
- 🛠️ [Tech Stack](#techstack)

## 📦 About

Wingfit is a minimalist fitness app to **plan your workouts**, **track your personal records** and **leverage smartwatch data**.

Demo is worth a thousand words, head to 📸 [Demo](#Demo).

🔒 Privacy-First – No telemetry, no tracking, fully self-hostable. You own your data. Inspect, modify, and contribute freely.

## 🌱 Getting Started

If you need help, feel free to open an [issue](https://github.com/itskovacs/wingfit/issues).

Deployment is designed to be simple using Docker.

## Option 1: Docker Compose (Recommended)

Use the `docker-compose.yml` file provided in this repository. No changes are required, though you may customize it to suit your needs.

Run the container:

```bash
docker-compose up -d
```

## Option 2: Docker Run

```bash

## Ensure you have the latest image

docker pull ghcr.io/itskovacs/wingfit:5

## Run the container

docker run -d -p 8080:8000 -v ./storage:/app/storage ghcr.io/itskovacs/wingfit:5
```

Refer to the [configuration documentation](https://github.com/itskovacs/wingfit/tree/main/docs/config.md) to set up OIDC authentication and other settings.

## 📸 Demo

A demo is available at [Wingfit.fr](https://wingfit.fr).

|         |         |
|:-------:|:-------:|
|  |  |
|  |  |
|  |  |

## 🚧 Roadmap

New features coming soonTM, check out the development plan in the [Roadmap Wiki](https://github.com/itskovacs/wingfit/wiki/Roadmap). If you have ideas 💡, feel free to open an issue.

If you want to develop new feature, feel free to open a pull request (see [🤝 Contributing](#contributing)).

## 📜 License

I decided to license Wingfit under the **CC BY-NC-SA 4.0** – You may use, modify, and share freely with attribution, but **commercial use is prohibited**.

## Key Resources

| Resource | Link |
|----------|------|
| issue | [https://github.com/itskovacs/wingfit/issues](https://github.com/itskovacs/wingfit/issues) |
| configuration documentation | [https://github.com/itskovacs/wingfit/tree/main/docs/config.md](https://github.com/itskovacs/wingfit/tree/main/docs/config.md) |
| Wingfit.fr | [https://wingfit.fr](https://wingfit.fr) |
| Roadmap Wiki | [https://github.com/itskovacs/wingfit/wiki/Roadmap](https://github.com/itskovacs/wingfit/wiki/Roadmap) |

