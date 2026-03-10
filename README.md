# Report Template

A template for creating report made with Quarto.

Public link to the report: https://technology-service-center.github.io/reporting-template/

## Getting Started

1. Install [Quarto CLI](https://quarto.org/docs/get-started/)
2. To edit the pages, modified the `.qmd` files. Edit `_quarto.yml` to change the layout of the website.

## Running Website Locally

Use the following command to run the website on your local device:

```
quarto preview
```

## Publicly Deploying the Website

1. Run the `quarto render` to render your website in the `/docs` folder.
2. Go to your repository setting > Pages. Under the "Build and deployment" section, select `Deploy from a branch` and set the branch to `/docs` folder.

## How to Copy Template to a New Repository

1. Clone your existing repository:

```
git clone [link to your existing repository]
```

2. Add the template repository as a remote.

```
git remote add template https://github.com/technology-service-center/reporting-template.git
```

3. Fetch the template repository data:

```
git fetch template
```

4. Copy files from the template's main branch into your current branch:

```
git checkout template/main -- .
```

5. Stage, commit the copied files, and then push to your own repository:

```
git add .
git commit -m "Add files from template repo"
git push origin main
```

## Resources

- [Quarto: Creating a Website](https://quarto.org/docs/websites/)
- [Github Docs: Markdown Syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Quarto: Github Pages](https://quarto.org/docs/publishing/github-pages.html)
