---
title: "Setting up Hugo for your custom domain"
date: 2023-09-03T18:53:50+02:00
draft: false
description: "I came across some fairly simple issues while I was setting up this website. It's better to make a note of these so that it is easier next time. It had to do with installing theme as a submodule and also setting the correct publishing source."
tags: [GitHub Pages, Hugo]
---

I had used Jekyll or Hugo some time ago. So this time when I setup this website, I had a couple of issues. It would be safe to say that there are some tasks that we think, are going to be easy but then it takes more time than intended.

I am going to list the main points here so that it is easier for my future self too.

This little blogpost assumes that the DNS record is set up correctly for your custom domain. You can go to this official GitHub doc to see the steps: [Configuring an apex domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)

## Installing the desired theme

When I was first setting up the theme I have on this site, I followed the steps which were mentioned on the relevant docs. It mentions just cloning the repository of the theme and editing the `hugo.toml` file to change the `theme` param. But it didn't work properly. The official [hugo quick start guide](https://gohugo.io/getting-started/quick-start/) mentions cloning the theme and adding it as a Git submodule. Consider it like a project within a project.

- Fix: Don't just clone the theme, add it as a submodule. Follow the official docs.

## Publishing source of your website

This took some time for me to understand. If you went to your website repository and then `Settings > Pages`, you can choose the branch and the folder from where the site will be built from.

If you already have a GitHub repository for your website, you might wanna do the following after you `cd` into your git repository.
    
    hugo new site .\ --force

instead of

    hugo new site quickstart

as shared in their official docs. 

You want all the directory structure in your current project and **NOT** in a separte folder inside your GitHub repo.

The last step would be to add the line to the `hugo.toml`

    publishDir = "docs"

The generated static files will then be stored in the above folder. This is important because if you see the `Pages` setting for your repository it gives you the option to choose the branch and folder. That's why we set it up to be docs. Just choose `docs`.

{{< figure src="https://raw.githubusercontent.com/psyklopp/AdityaBhardwaj-dev/main/images/docs_publish_site.png" title="Publishing source for your website" >}}

## Using GitHub for hosting images

This is the most simple yet the most stupid mistake I made. The `hugo.toml` file has the `favicon` param which has to be the link to the image file (of course for the favicon). I updated the path to the image like this `https://github.com/psyklopp/AdityaBhardwaj-dev/blob/main/favicon.png`. You can probably tell this opens the page to the github page and NOT the image directly.


- Fix: Open the image in a separate tab and then copy the image address. It looks something like this: `https://raw.githubusercontent.com/psyklopp/AdityaBhardwaj-dev/main/favicon.png`. Yes, that's the link to my favicon.

I know, trivial but something I will keep in mind.

-----