# Intro
ZJU 22 SE
UIUC 25Fall ECE MEng

The course notes are for reference only; please point out any errors.

Some repositories contain corresponding [PDF versions](https://github.com/CindyZhou2003/mymkdocs/tree/master/docs/pdf).

Not for commercial use.

## Technical Notes

I maintain this notebook as a collection of lecture notes and exam reviews from my coursework at Zhejiang University and the University of Illinois Urbana-Champaign. I add new material and revise earlier notes as I revisit topics such as machine learning, distributed systems, and parallel programming.

## Deployment

Every push to `master` triggers the [GitHub Actions deployment workflow](.github/workflows/deploy.yml). The workflow checks out the full Git history so MkDocs can display each page's last-updated date, installs Material for MkDocs and its plugins, and runs `mkdocs gh-deploy --force` to build the site and publish it to the `gh-pages` branch. The notebook is available on [GitHub Pages](https://cindyzhou2003.github.io/mymkdocs/).
