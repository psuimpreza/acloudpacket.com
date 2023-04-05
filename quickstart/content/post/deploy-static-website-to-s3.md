---
title: "Deploying a Static Website to S3 using GitHub Actions"
subtitle:    ""
description: ""
date: 2022-12-29
author:      ""
image:       ""
tags:        ["Hugo", "Static Web Site", "Git", "Github", "Github Actions", "AWS", "S3"]
categories:  ["Web" ]
draft: false


---
To create a static website using Hugo, GitHub, GitHub Actions, and Amazon S3, follow these steps:

    Install Hugo:

    If you are using macOS or Linux, you can install Hugo using the following command:
    brew install hugo
    If you are using Windows, you can download the latest Hugo executable from the Hugo releases page and add it to your PATH.

    Create a new Hugo site:

    Navigate to the directory where you want to create your new Hugo site and run the following command:
    hugo new site mysite
    This will create a new Hugo site in a directory called mysite.

    Choose a Hugo theme:

    Hugo has a large collection of themes available. You can browse the themes and find one that suits your needs.
    To add a theme to your site, clone the theme repository into the themes directory of your site:
    git clone https://github.com/<USERNAME>/<THEME_REPO> themes/<THEME_NAME>
    Then, specify the theme in your site's config.toml file:
    theme = "<THEME_NAME>"

    Create content:

    You can create new content for your site using the hugo new command. For example, to create a new blog post:
    hugo new posts/my-first-post.md
    This will create a new Markdown file in the content/posts directory. You can edit this file to add the content for your blog post.

    Preview your site:

    You can preview your site by running the following command:
    hugo server -D
    This will start a local development server at http://localhost:1313, where you can preview your site.

    Deploy your site:

    You can use GitHub and GitHub Actions to build and deploy your site automatically.
    First, create a new repository on GitHub and push your site's code to it.
    Then, create a new file in the .github/workflows directory called deploy.yml. This file will contain the configuration for your GitHub Action.
    In the deploy.yml file, add the following content:

name: Deploy

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build site
        run: hugo
      - name: Deploy to S3
        uses: aws-actions/aws-s3-deploy@v1
        with:
          bucket: mysite-bucket
          region: us-east-1
          local_dir: public
          acl: public-read
          create_bucket: true
          delete_removed: true
          profile: my-aws-profile

    This action will build your site using Hugo when you push to the master branch and then deploy the built site to an Amazon S3 bucket called mysite-bucket. You will need to replace `mysite-bucket