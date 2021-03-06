---
title: github.io 블로그 포스팅 시 참고
author: Seho Kim
date: 2020-08-09 10:41:00 +0800
categories: [Github]
tags: [github]
pin: true
---

## github.io 블로그 포스팅 시 참고 글

- [POST 새로 추가하기(제공된 Bash shell 활용)](https://github.com/cotes2020/jekyll-theme-chirpy/wiki/Writing-a-new-post)

```terminal
$ git clone git@github.com:<username>/jekyll-theme-chirpy -b master --single-branch
```

### Setting up the local envrionment

If you would like to run or build the project on your local machine, please follow the [Jekyll Docs](https://jekyllrb.com/docs/installation/) to complete the installation of `Ruby`, `RubyGems` and `Bundler`. 

`bundle` will automatically install all the dependencies specified by `Gemfile`.

What's more, in order to generate some extra files (*categories*, *tags* and *last modified list*), we need to use some tool scripts. If your machine is running Debian or macOS, make sure that [GNU coreutils](https://www.gnu.org/software/coreutils/) is installed. Otherwise, install by:

* Debian

  ```console
  $ sudo apt-get install coreutils
  ```

> If you not intend to deploy it on GitHub Pages, append parameter option `--no-gh` at the end of the above command.

1. Remove some files or directories from your repository:
    - `.travis.yml`
    - everything under `.github/`
    - files under `_posts/`
    - folder `docs/` 

### Configuration

Generally, go to `_config.yml` and configure the variables as needed. Some of them are typical options:
* `url`
* `avatar`
* `timezone`
* `theme_mode`


Then open a browser and visit to <http://localhost:4000>.

### Deployment

Before the deployment begins, checkout the file `_config.yml` and make sure the `url` is configured correctly. Furthermore, if you prefer the [_project site_](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) and don't use a custom domain, or you want to visit your website with a base url on a web server other than **GitHub Pages**, remember to change the `baseurl` to your project name that starting with a slash. For example, `/project`.

Assuming you have already gone through the [initialization](#initialization), you can now choose any of the following methods to deploy your website.

#### Deploy on GitHub Pages

For security reasons, GitHub Pages build runs on `safe` mode, which restricts us from using tool scripts to generate additional page files. Therefore, we can use GitHub Actions to build the site, store the built site files on a new branch, and use that branch as the source of the Pages service.

1. Push any commit to `origin/master` to trigger the GitHub Actions workflow. Once the build is complete, a new remote branch called `gh-pages` will appear, which is used to store the built site files.

2. Unless you prefer to project sites, rename your repository to `<username>.github.io` on GitHub.

3. Choose branch `gh-pages` as your GitHub Pages source.

4. Visit your website at the address indicated by GitHub.

#### Deploy on Other Platforms

On platforms other than GitHub, e.g. GitLab, we cannot enjoy the convenience of **GitHub Actions**. However, we have a tool to make up for this shortcoming.

Commit the changes of your repository first, then run the publish script:

```console
$ bash tools/publish.sh
```

> Please note that the *Recent Update* list requires the latest git-log date of posts, thus make sure the changes in `_posts` have been committed before running this command.

It will automatically generates the *Latest Modified Date* and *Categories / Tags* page for the posts and submit a commit, then push to `origin/master`. Its output is similar to the following log:

```terminal
[INFO] Success to update lastmod for 4 post(s).
[INFO] Succeed! 3 category-pages created.
[INFO] Succeed! 4 tag-pages created.
[INFO] Published successfully!
```

Lastly, enable the pages service according to the instructions of the platform you choose.

#### Deploy on Private Server

In the root of the source project, build your site by:

```console
$ bash tools/build.sh -d /path/to/site/
```

The generated site files will be placed in the root of `/path/to/site/`. Now you should upload those files to your web server, such as Nginx.
