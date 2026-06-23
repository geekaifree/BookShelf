# nyum

**Source:** https://github.com/doersino/nyum

## Overview

This tutorial covers the key resources and tools from the [doersino/nyum](https://github.com/doersino/nyum) project.

## nyum

*A simple Pandoc-powered static site generator for your recipe collection.*

This tool takes a **collection of Markdown-formatted recipes** and turns it into a **lightweight, responsive, searchable website** for your personal use as a reference while cooking, or for sharing with family and friends. It's *not* intended as a cooking blog framework – there's no RSS feed, no social sharing buttons, and absolutely zero SEO.

📓 Think of it as a **cookbook for nerds**.

Below the screenshots, you'll find some notes on [setting this tool up](#setup), [running it](#building), [formatting your recipes](#formatting), and [deploying the generated site](#deployment).

## Screenshots

If you prefer a live website over the following screenshots, feel free to **check out the [demo on GitHub Pages](https://ghpages.noahdoersing.com/nyum/_site/index.html)**!

On an old-fashioned computer, a [recipe](https://ghpages.noahdoersing.com/nyum/_site/cheesebuldak.html) might look more or less like this – notice the little star indicating that this is a favorite!

Below, on the right, is the same page shown at tablet scale. More interestingly, the index page is shown on the left (with an active search) – note that you can, of course, customize the title and description.

Finally, more of the same on three phone-sized screens. The three-column layout doesn't fit here, so instructions are shown below ingredients. And *of course* the light's turned off if you've enabled dark mode on your device.

## Setup

First off, either `git clone` this repository or [download it as a ZIP](https://github.com/doersino/nyum/archive/refs/heads/main.zip). (You can clear out the `_recipes/` and `_site/` directories to get rid of the demo data.)

I don't like complicated dependency trees and poorly-documented build processes, so here's an **exhaustive list of the dependencies** you're not overwhelmingly likely to already have:

* [Pandoc](https://pandoc.org) – version 2.8 (released in November 2019) or later *(earlier versions don't support partials/subtemplates)*.

    On macOS, assuming you're using [Homebrew](https://brew.sh), `brew install pandoc` will do the trick. On Linux, your package manager almost certainly has it (although the version it provides might be outdated – recent binaries are available [here](https://github.com/jgm/pandoc/releases/latest)).

That's it, only one dependency! Hooray!

(Since `build.sh` relies on some Bash-specific bits and bobs and ubiquitous POSIX utilities like `awk` and `tee`, you'll also need those – but since Bash the default shell on most non-Windows systems, you're likely running it already. If you're a Windows user, don't despair: Through the magic of [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and possibly [some Git or text editor reconfiguration to deal with line endings](https://github.com/doersino/nyum/issues/10), it's definitely possible to run this tool. If you run into trouble, feel free to [file an issue](https://github.com/doersino/nyum/issues), but know that I might be unable to offer much well-founded advice.)

## Configuration

Open `config.yaml` in whichever text editor you heart is drawn to in the moment and follow the instructions in the comments. There's not actually very much to configure.

You can, for example, change the language of your site. There's also a setting `show_images_on_index` (whose name obviates any need for further explanation).

## Building

Run `bash build.sh`.

(It accepts a few optional flags, notably `--help` which tells you about the rest of them.)

## Formatting

TL;DR: See the example recipes in `_recipes/`.

Each recipe **begins with YAML front matter specifying its title**, how many servings it produces, whether it's spicy or vegan or a favorite, the category, an image (which must also be located in the `_recipes/` directory), and other information. Scroll down a bit for a list of possible entries – most of these are optional!

The **body of a recipe consists of horizontal-rule-separated steps, each listing ingredients relevant in that step along with the associated instruction**. Ingredients are specified as an unordered list, with ingredient amounts enclosed in backticks (this enables the columns on the resulting website – if you don't care about that, omit the backticks). The instructions must be preceded with a `>`. Note that a step can also solely consist of an instruction.

*You've got the full power of Markdown at your disposal – douse your recipes in [formatting](https://github.com/doersino/nyum/blob/main/_recipes/kkaennipjeon.md), include a picture for each step, and use the garlic emoji as liberally as you should be using garlic in your cooking!*

(Before building this tool, I had been using a custom LaTeX template built on top of the [cuisine](https://ctan.org/pkg/cuisine?lang=en) package, which enforces a three-column, relevant-ingredients-next-to-instructions structure. [In the process of graduating from university, I found myself contemporaneously graduating from wanting to use LaTeX for everything, which was part of the impetus for building this tool.] I've found this structure to be more useful than the more commonly found all-ingredients-first-then-a-block-of-instructions approach.)

## Example

```markdown
---
title: Cheese Buldak
original_title: 치즈불닭
category: Korean Food
description: Super-spicy chicken tempered with loads of cheese and fresh spring onions. Serve with rice and a light salad – or, better yet, an assortment of side dishes.
image: cheesebuldak.jpg
size: 2-3 servings
time: 1 hour
author: Maangchi
source: https://www.youtube.com/watch?v=T9uI1-6Ac6A
spicy: ✓
favorite: ✓
---

* `2 tbsp` chili flakes (gochugaru)
* `1 tbsp` gochujang
* `½-⅔ tbsp` soy sauce
* `1 tbsp` cooking oil
* `¼ tsp` pepper
* `2-3 tbsp` rice or corn syrup
* `2 tbsp` water

> Mix in an oven-proof saucepan or cast-iron skillet – you should end up with a thick marinade.

---

* `3-4 cloves` garlic
* `2 tsp` ginger

> Peel, squish with the side of your knife, then finely mince and add to the marinade.

---

> ⋯ (omitted for brevity)

---

> Garnish with the spring onion slices and serve.

```

## YAML front matter

You *must* specify a non-empty value for the `title` entry. Everything else is optional:

* `original_title`: Name of the recipe in, say, its country of origin.
* `category`: Self-explanatory. Recipes belonging to the same category will be grouped on the index page. Don't name a category such that the generated category page will have the same URL as a recipe.
* `description` A short description of the dish, it will be shown on the index page as well.
* `nutrition`: Allows you to note down some nutrition facts for a recipe. Must take the form of a list, for example:
    ```yaml
    nutrition:
      - 300 calories
      - 60 g sugar
      - 0.8 g fat
      - 3.8 g protein
    ```
* `image`: Filename of a photo of the prepared dish, *e.g.*, `strawberrysmoothie.jpg`. The image must be located *alongside* the Markdown document – not in a subdirectory, for instance.
* `image_attribution` and `image_source`: If you haven't created the recipe photo yourself, you might be required to attribute its author or link back to its source (which should be an URL). The attribution, if set, will be shown semi-transparently in the bottom right corner of the image. If the source is non-empty, a click on the image will take you there.
* `size`: How many servings does the recipe produce, or how many cupcakes does it yield, or does it fit into a small or large springform?
* `time`: Time it takes from getting started to serving.
* `author`: Your grandma, for example.
* `source`: Paste the source URL here if the recipe is from the internet. If set, this will turn the `author` label into a link. If no author is set, a link labelled "Source" will be shown.
* `favorite`: If set to a non-empty value (*e.g.*, "✓"), a little star will be shown next to the recipe's name. It'll also receive a slight boost in search results.
* `veggie` and `vegan`: Similar and self-explanatory. If *neither* of these is set to a non-empty value, a "Meat" label will be shown.
* `spicy`, `sweet`, `salty`, `sour`, `bitter`, and `umami`: Similar – if set to a non-empty value, a colorful icon will be shown.

## Deployment

After running `build.sh`, **just chuck the contents of `_site/` onto a server of your choice**.

## Key Resources

| Resource | Link |
|----------|------|
| demo on GitHub Pages | [https://ghpages.noahdoersing.com/nyum/_site/index.html](https://ghpages.noahdoersing.com/nyum/_site/index.html) |
| recipe | [https://ghpages.noahdoersing.com/nyum/_site/cheesebuldak.html](https://ghpages.noahdoersing.com/nyum/_site/cheesebuldak.html) |
| download it as a ZIP | [https://github.com/doersino/nyum/archive/refs/heads/main.zip](https://github.com/doersino/nyum/archive/refs/heads/main.zip) |
| Pandoc | [https://pandoc.org](https://pandoc.org) |
| Homebrew | [https://brew.sh](https://brew.sh) |
| here | [https://github.com/jgm/pandoc/releases/latest](https://github.com/jgm/pandoc/releases/latest) |
| WSL | [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10) |
| some Git or text editor reconfiguration to deal with line endings | [https://github.com/doersino/nyum/issues/10](https://github.com/doersino/nyum/issues/10) |
| file an issue | [https://github.com/doersino/nyum/issues](https://github.com/doersino/nyum/issues) |
| formatting | [https://github.com/doersino/nyum/blob/main/_recipes/kkaennipjeon.md](https://github.com/doersino/nyum/blob/main/_recipes/kkaennipjeon.md) |
| cuisine | [https://ctan.org/pkg/cuisine?lang=en](https://ctan.org/pkg/cuisine?lang=en) |
| enable GitHub Pages | [https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) |
| file an issue | [https://github.com/doersino/nyum/issues](https://github.com/doersino/nyum/issues) |
| file an issue | [https://github.com/doersino/nyum/issues](https://github.com/doersino/nyum/issues) |
| file an issue | [https://github.com/doersino/nyum/issues](https://github.com/doersino/nyum/issues) |
| an issue | [https://github.com/doersino/nyum/issues/1](https://github.com/doersino/nyum/issues/1) |
| Grimgrains | [https://github.com/hundredrabbits/GrimGrains](https://github.com/hundredrabbits/GrimGrains) |
| even more Instagram-worthy | [https://www.instagram.com/p/B6vQOHDiySF/](https://www.instagram.com/p/B6vQOHDiySF/) |
| Monami Curry, Yongsan-gu, Seoul | [https://www.google.com/maps/place/Monami+Curry+Seoul/@37.5298686,126.9707568,15z/data=!4m5!3m4!1s0x0:0x6ce40a80f13a74d5!8m2!3d37.5298686!4d126.9707568](https://www.google.com/maps/place/Monami+Curry+Seoul/@37.5298686,126.9707568,15z/data=!4m5!3m4!1s0x0:0x6ce40a80f13a74d5!8m2!3d37.5298686!4d126.9707568) |
| **Barlow** | [https://github.com/jpt/barlow](https://github.com/jpt/barlow) |
| **Lora** | [https://github.com/cyrealtype/Lora-Cyrillic](https://github.com/cyrealtype/Lora-Cyrillic) |
| **Tabler Icons** | [https://tabler-icons.io](https://tabler-icons.io) |
| Facebook Design | [https://design.facebook.com/toolsandresources/devices/](https://design.facebook.com/toolsandresources/devices/) |
| Google Maps screenshot of a rare earth mining operation in China | [https://www.google.com/maps/@40.4448594,90.8008231,21196m/data=!3m1!1e3](https://www.google.com/maps/@40.4448594,90.8008231,21196m/data=!3m1!1e3) |
| Markdeep Diagram Drafting Board | [https://ghpages.noahdoersing.com/markdeep-diagram-drafting-board/](https://ghpages.noahdoersing.com/markdeep-diagram-drafting-board/) |

