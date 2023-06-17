# Introduction

MkDocs is a popular static site generator specifically designed for creating documentation websites. It allows you to write your documentation content in Markdown format and automatically generates a static HTML website.

Here are a few reasons why MkDocs is a good choice for technical documentation:

- **Simplicity**
It has a minimalistic approach, focusing on the essentials of documentation without unnecessary complexity.

- **Markdown support**
With MkDocs, you can write your documentation content in Markdown, making it accessible to both technical and non-technical contributors.

- **Navigation and search**
MkDocs automatically generates a navigation menu based on the directory structure of your documentation. Additionally, it provides a built-in search functionality that allows users to quickly find the information they need within your documentation.

- **Customizability**
MkDocs offers a range of customizable themes and templates, allowing you to tailor the appearance of your documentation to match your brand or project.

- **Versioning and deployment**
MkDocs supports versioning, making it convenient to manage and publish multiple versions of your documentation.

- **Integration with version control systems (VCS)**
MkDocs works well with VCS like Git. You can store your documentation files in a Git repository, making it easy to collaborate with team members, track changes, and manage contributions.

In this document, I share the process of building an MkDoc static website and hosting in on GitHub pages.

# Pre-requisites

- VS Code (or other source code editor)
- Python extension installed
- GitHub account
- GiHub desktop

# **Step-by-step guides**

The instructions below help create a GitHub repository, clone the repository to the local machine, launch the MkDocs website with Python, and publish it to GitHub pages.

## **Create GitHub repository**

To create new repository in your GitHub account

1. Log in to your GitHub account.
2. At the top left corner, select **+** > **New repository**.
3. Give a name to your repository.
4. Select **Public**.
5. Select **Add a README file**.
6. For **.gitignore** select **Python**.
7. (Optional) For the **Choose a license** step, select the **GNU General pulic license** from the dropdown list.
8. Select **Create repository**.
Your repository has been created.
9. Open your GitHub desktop account and [clone the repository](https://www.youtube.com/watch?v=PoZNIbs_wx8).

Now you can make changes locally and then commit and push them to GitHub account in the web.

## **Build website**

**To build a website**

1. Open your cloned project in VS Code and open its terminal.
2. Assuming you have Python already, create virtual Python environment by using the following command:

    ```py
   python -m venv venv
    ```

3. Activate it using the following command:

    ```py
   source venv/bin/activate
    ```

4. Install MkDocs with the following command:

    ```py
   pip install mkdocs-material
    ```

    All the dependancies are downloaded for the website.
5. Created a new website by using the command:

    ```py
   mkdocs new .
    ```

    You  now have two files created for the website:

    ```py
    INFO     -  Writing config file: ./mkdocs.yml
    INFO     -  Writing initial docs: ./docs/index.md
    ```

6. Run the website locally by using the command:

    ```py
   mkdocs serve
    ```

    You know have a website built and serving on the local host ```http://127.0.0.1:8000/```

7. Open the website by copying and pasting the local host address into the browser address bar.
The website is served and can be accesses locally.
![Starting page](mkdocs_basic.jpg)

If make a pause and need to activate the env some time later, use the following commands in the VS Code terminal of the project:

```py
source venv/bin/activate

mkdocs serve
```

## **Configure website**

The website has the starting configuration. You can add configuration using the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/) documentation. Let us proceed with the basic setup.

**To configure mkdocs website**

1. Open your mkdocs.yml in VS Code.
2. Edit the content to change theme, define language, add a search box, and set colours:

    ```yml
    site_name: Your website name
     theme: 
      name: material
      features:
        - navigation.tabs
        - navigation.sections
        - toc.integrate
        - navigation.top
        - search.suggest
        - search.highlight
        - content.tabs.link
        - content.code.annotation
        - content.code.copy
        - toc.follow
        - navigation.path
      language: en
      palette:
        - scheme: default
        toggle:
            icon: material/toggle-switch-off-outline 
            name: Switch to dark mode
        primary: indigo
        accent: purple 
        - scheme: slate 
        toggle:
            icon: material/toggle-switch
            name: Switch to light mode    
        primary: indigo
        accent: lime
    ```

3. Save changes to apply the changes.
4. Use the following command to rerun the website configuration:

    ```py
    mkdocs serve
    ```

    When you refresh the website in your browser by visiting the same local host, you can see the changes. If you need to add more settings to your website configuration and add extensions, use the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/) documentation.

## **Add pages**

**To add pages**

1. Go to the project folder in VS Code.
2. Select the **docs** folder.
3. Select **New file**.
4. Enter the file name and define the .md format.
For example, **anotherpage**.**md**.
5. Save your file and open it.
6. Add the text to be displayed on the newly added page.
7. Save the changes.
When you refresh the page, you can see the changes.
![Changed](mkdocs_changes.jpg)

## **Publish website on GitHub**

**To prepare files for publishing**

1. Open your website project in VS code.
2. Create the **.github** folder.
3. In the **.github** folder, create the **workflows** folder.
4. In the the **workflows** folder, create **ci.yml** file.
5. Paste the following code to the file:

    ```yml
    name: ci 
    on:
    push:
    branches:
      - master 
      - main
    permissions:
    contents: write
    jobs:
    deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - uses: actions/cache@v2
        with:
          key: ${{ github.ref }}
          path: .cache
      - run: pip install mkdocs-material
      - run: pip install pillow cairosvg
      - run: mkdocs gh-deploy --force
    ```

6. Save changes.
7. Open you GitHub Desktop, add comment and commit changes to GitHub.
8. Select **Push origin** to push changes to the origin remote repository.
The website project files are now stored on GitHub.

**To publish website using GitHub pages**

1. On GitHub, open the project repository.
2. Go to **Settings** > **Pages**.
3. For **Source**, leave **Deploy from a branch**.
4. For **Branch**, select **gh-pages** and save.
![GitHub](mkdocs_github.jpg)
5. Go to the **Actions** tab.
You can see that the website is being deployed to GitHub pages.
6. Open the **pages build and deployment** and follow the link in **deploy** box.
The website is published.
7. Add a direct link to the repository **About** section by opening settings, selecting the **Use your GitHub Pages website** checkbox, and saving the changes.
![Link](mkdocs_link.jpg)

You can know access your website and share it with others, make changes locally and push them to GitHub. The website is automatically deployed after you push your changes.

---

**Check the following references for more information:**

- [MkDocs documentation](https://squidfunk.github.io/mkdocs-material/)
- [GitHub pages](https://pages.github.com/)
- [Code blocks in MkDocs](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/)
