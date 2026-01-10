# Earl's Blog Development Guide

Welcome to the development guide for Earl's Blog. This document provides everything you need to know to manage, update, and maintain the blog content.

## Table of Contents

1.  [Getting Started: Running the Site Locally](#1-getting-started-running-the-site-locally)
2.  [Managing Blog Posts](#2-managing-blog-posts)
    -   [Adding a New Post](#adding-a-new-post)
    -   [Understanding the Frontmatter](#understanding-the-frontmatter)
    -   [Writing Content with Markdown](#writing-content-with-markdown)
3.  [Understanding the Project Structure](#3-understanding-the-project-structure)
    -   [How File-Based Routing Works](#how-file-based-routing-works)
    -   [How Layouts Work](#how-layouts-work)
4.  [Making Customizations](#4-making-customizations)
    -   [Editing Content](#editing-content)
    -   [Changing Page Order](#changing-page-order)
    -   [Changing Styles (CSS)](#changing-styles-css)
    -   [Changing the Site Layout (HTML)](#changing-the-site-layout-html)
5.  [Saving and Publishing Changes](#5-saving-and-publishing-changes)
    -   [Pulling Changes from Other Contributors](#pulling-changes-from-other-contributors)
    -   [Developing Locally](#developing-locally)
    -   [Deploying Changes to the Live Site](#deploying-changes-to-the-live-site)

---

## 1. Getting Started: Running the Site Locally

To see your changes on your computer before publishing them, you need to run a local development server. This allows you to preview the website in your browser.

1.  **Open a terminal or command prompt.**
2.  **Install dependencies:** The first time you set up the project, you need to install the necessary software packages. Run this command:
    ```bash
    bun install
    ```
3.  **Start the development server:** Once the installation is complete, run the following command:
    ```bash
    bun run dev
    ```
4.  **View your site:** The terminal will show a local address, usually `http://localhost:4321`. Open this URL in your web browser to see a live preview of the site. The server will automatically update the site as you save your changes.

---

## 2. Managing Blog Posts

All blog posts are stored as `.mdx` files in the `src/content/posts/` directory.

### Adding a New Post

1.  Navigate to the `src/content/posts/` directory in the project.
2.  Create a new file. The file name should be descriptive, in `kebab-case` (all lowercase with words separated by dashes), and end with `.mdx`.
    -   *Example:* `2024-my-new-adventure.mdx`
3.  Copy and paste the following template into your new file. This is the "frontmatter" and is required for every post.

    ```yaml
    ---
    title: "Your Post Title Here"
    description: "A short, one-sentence description of your blog post."
    postDate: YYYY-MM-DD
    laytout: '@/layouts/ArticleLayout.astro'
    ---

    (Start writing your blog post content here using Markdown...)
    ```

4.  Fill out the frontmatter fields and start writing your post below the `---`.

### Understanding the Frontmatter

The section at the very top of the `.mdx` file, enclosed in `---`, is called frontmatter. It's a set of key-value pairs that define metadata for your post.

-   `title`: (Required) The main title of your blog post. This is what will be displayed at the top of the page and in the browser tab.
-   `postDate`: (Required) The publication date of the post. **This is very important as it controls the order in which posts appear on the site.** The format must be `YYYY-MM-DD`.
-   `description`: (Required) A brief summary of the post. This is used for search engine optimization (SEO) and for preview text on listing pages.
-   `laytout`:  generally use the following value: '@/layouts/ArticleLayout.astro' This specifies the layout for the post.

### Writing Content with Markdown

The body of your post is written using Markdown, a simple syntax for formatting text. You can create headings, lists, bold/italic text, links, images, and more.

For a complete guide on how to use Markdown, refer to this excellent cheat sheet:
**[Markdown Guide Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)**

---

## 3. Understanding the Project Structure

This website is built with a framework called Astro, which uses a simple but powerful file-based structure.

### How File-Based Routing Works

The website's URLs are determined by the file and folder structure within `src/content/posts/`.

-   Every `.mdx` file you create in `src/content/posts/` automatically becomes a blog post page.
-   The file `src/content/posts/2024-my-new-adventure.mdx` will be accessible at the URL `/posts/2024-my-new-adventure`.
-   The logic that handles this is located in `src/pages/posts/[...slug].astro`. You do not need to edit this file, but it is what finds your markdown file and renders it as a page.

### How Layouts Work

Layouts are templates that wrap your content, ensuring a consistent look and feel across the site.

-   `src/layouts/Layout.astro`: This is the main layout for the entire site. It contains the core HTML structure, including the `<head>`, header, and footer that appear on every page.
-   `src/layouts/ArticleLayout.astro`: This layout is specifically for blog posts. It uses the main `Layout.astro` and adds styling and structure specific to articles. Your markdown content is injected into this layout.

---

## 4. Making Customizations

Here’s where to go to make common changes.

### Editing Content

To edit an existing blog post, simply find its corresponding `.mdx` file in the `src/content/posts/` directory and make your changes.

### Changing Page Order

The order of blog posts on the main page is determined by the `postDate` in each post's frontmatter.

-   To move a post to the top of the list, give it a more recent date.
-   To move a post down, give it an older date.

### Changing Styles (CSS)

Styling is done using CSS. The styles for this site are primarily located inside `<style>` tags within the layout files.

-   **For blog post-specific styles:** Go to `src/layouts/ArticleLayout.astro`. You will find a `<style>` block at the bottom of the file where you can change fonts, colors, and spacing for the article content.
-   **For global styles that affect the entire site:** Go to `src/layouts/Layout.astro`. The `<style>` block here controls the overall appearance.

### Changing the Site Layout (HTML)

If you need to change the fundamental structure of the pages (e.g., add a new element to the header or footer), you will need to edit the layout files.

-   **For the overall site structure:** Edit the HTML in `src/layouts/Layout.astro`.
-   **For the structure of blog post pages:** Edit the HTML in `src/layouts/ArticleLayout.astro`.

---

## 5. Saving and Publishing Changes

This project uses `git` for version control and `bun` for running scripts. Here is the complete workflow for making and publishing changes.

### Pulling Changes from Other Contributors

Before you start working, it's a good practice to make sure you have the latest version of the site.

```bash
bun run pull
```
This command fetches and merges any changes made by others.

### Developing Locally

As described in section 1, use this command to preview your work.

```bash
bun run dev
```

### Deploying Changes to the Live Site

Once you are happy with your changes, you can deploy them to the live website. The following command automates the entire process: building the site, saving your changes, and publishing them.

1.  Make sure you have saved all your file edits.
2.  Run the deploy command in your terminal:
    ```bash
    bun run deploy
    ```
