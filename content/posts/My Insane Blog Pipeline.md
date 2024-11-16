---
title: My Insane Blog Pipeline
date: 2024-11-15
draft: false
tags:
  - networkchuck
  - blog
---
# Obsidian

- Obsidian is the BEST notes application in the world. Go download it: https://obsidian.md/

## The Setup

- Create a new folder labeled *posts*. This is where you will add your blog posts
- ....that's all you have to do
- Actually...wait....find out where your Obsidian directories are. Right click your *posts* folder and choose *show in system explorer*
- You'll need this directory in upcoming steps.


!![Image Description](/images/Pasted%20image%2020241115145036.png)


# Setting up Hugo

## Install Hugo

### Prerequisites

- Install Git: https://github.com/git-guides/install-git
- Install Go: https://go.dev/dl/

### Install Hugo

Link: https://gohugo.io/installation/


### Create a new site

```bash
## Verify Hugo works
hugo version

## Create a new site 

hugo new site websitename
cd websitename
```


### Download a Hugo Theme

- Find themes from this link: https://themes.gohugo.io/
	- *follow the theme instructions on how to download. The BEST option is to install as a git submodule*

```bash
## Initialize a git repository (Make sure you are in your Hugo website directory)

git init

## Set global username and email parameters for git

git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"


## Install a theme (we are installing the Terminal theme here). Once downloaded it should be in your Hugo themes folder
## Find a theme ---> https://themes.gohugo.io/

git submodule add -f https://github.com/panr/hugo-theme-terminal.git themes/terminal

```

### Adjust Hugo settings

- Most themes you download will have an example configuration you can use. This is usually the best way to make sure Hugo works well and out of the box. 
- For the *Terminal* theme, they gave this example config below. 
- We will edit the *hugo.toml* file to make these changes. ----> `nano hugo.toml` (Linux/Mac) or `notepad hugo.toml` (Windows) or `code hugo.toml` (All platforms)

```toml
baseurl = "/"
languageCode = "en-us"
# Add it only if you keep the theme in the `themes` directory.
# Remove it if you use the theme as a remote Hugo Module.
theme = "terminal"
paginate = 5

[params]
  # dir name of your main content (default is `content/posts`).
  # the list of set content will show up on your index page (baseurl).
  contentTypeName = "posts"

  # if you set this to 0, only submenu trigger will be visible
  showMenuItems = 2

  # show selector to switch language
  showLanguageSelector = false

  # set theme to full screen width
  fullWidthTheme = false

  # center theme with default width
  centerTheme = false

  # if your resource directory contains an image called `cover.(jpg|png|webp)`,
  # then the file will be used as a cover automatically.
  # With this option you don't have to put the `cover` param in a front-matter.
  autoCover = true

  # set post to show the last updated
  # If you use git, you can set `enableGitInfo` to `true` and then post will automatically get the last updated
  showLastUpdated = false

  # Provide a string as a prefix for the last update date. By default, it looks like this: 2020-xx-xx [Updated: 2020-xx-xx] :: Author
  # updatedDatePrefix = "Updated"

  # whether to show a page's estimated reading time
  # readingTime = false # default

  # whether to show a table of contents
  # can be overridden in a page's front-matter
  # Toc = false # default

  # set title for the table of contents
  # can be overridden in a page's front-matter
  # TocTitle = "Table of Contents" # default


[params.twitter]
  # set Twitter handles for Twitter cards
  # see https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started#card-and-content-attribution
  # do not include @
  creator = ""
  site = ""

[languages]
  [languages.en]
    languageName = "English"
    title = "Terminal"

    [languages.en.params]
      subtitle = "A simple, retro theme for Hugo"
      owner = ""
      keywords = ""
      copyright = ""
      menuMore = "Show more"
      readMore = "Read more"
      readOtherPosts = "Read other posts"
      newerPosts = "Newer posts"
      olderPosts = "Older posts"
      missingContentMessage = "Page not found..."
      missingBackButtonLabel = "Back to home page"
      minuteReadingTime = "min read"
      words = "words"

      [languages.en.params.logo]
        logoText = "Terminal"
        logoHomeLink = "/"

      [languages.en.menu]
        [[languages.en.menu.main]]
          identifier = "about"
          name = "About"
          url = "/about"
        [[languages.en.menu.main]]
          identifier = "showcase"
          name = "Showcase"
          url = "/showcase"
```

### Test Hugo

```bash
## Verify Hugo works with your theme by running this command

hugo server -t themename
```

# Walking Through the Steps

*NOTE: There is a MEGA SCRIPT later in this blog that will do everything in one go.*

## Syncing Obsidian to Hugo

### Windows

```powershell
robocopy sourcepath destination path /mir
```

### Mac/Linux

```bash
rsync -av --delete "sourcepath" "destinationpath"
```


## Add some frontmatter

```bash
---
title: blogtitle
date: 2024-11-06
draft: false
tags:
  - tag1
  - tag2
---
```


## Transfer Images from Obsidian to Hugo


### Windows

```python
import os
import re
import shutil

# Paths (using raw strings to handle Windows backslashes correctly)
posts_dir = r"C:\Users\chuck\Documents\chuckblog\content\posts"
attachments_dir = r"C:\Users\chuck\Documents\my_second_brain\neotokos\Attachments"
static_images_dir = r"C:\Users\chuck\Documents\chuckblog\static\images"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)
        
        with open(filepath, "r", encoding="utf-8") as file:
            content = file.read()
        
        # Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)
        
        # Step 3: Replace image links and ensure URLs are correctly formatted
        for image in images:
            # Prepare the Markdown-compatible link with %20 replacing spaces
            markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)
            
            # Step 4: Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)

        # Step 5: Write the updated content back to the markdown file
        with open(filepath, "w", encoding="utf-8") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")
```


### Mac/Linux

```python
import os
import re
import shutil

# Paths
posts_dir = "/Users/networkchuck/Documents/chuckblog/content/posts/"
attachments_dir = "/Users/networkchuck/Documents/neotokos/Attachments/"
static_images_dir = "/Users/networkchuck/Documents/chuckblog/static/images/"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)
        
        with open(filepath, "r") as file:
            content = file.read()
        
        # Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)
        
        # Step 3: Replace image links and ensure URLs are correctly formatted
        for image in images:
            # Prepare the Markdown-compatible link with %20 replacing spaces
            markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)
            
            # Step 4: Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)

        # Step 5: Write the updated content back to the markdown file
        with open(filepath, "w") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")
```


# Setup GitHub

- Git yourself an account
- Then create a repo

## Authenticate yourself

```bash
## Generate an SSH key (Mac/Linux/Windows)

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

```


## Push to GitHub

```bash
# Step 8: Push the public folder to the hostinger branch using subtree split and force push
echo "Deploying to GitHub Hostinger..."
git subtree split --prefix public -b hostinger-deploy
git push origin hostinger-deploy:hostinger --force
git branch -D hostinger-deploy
```