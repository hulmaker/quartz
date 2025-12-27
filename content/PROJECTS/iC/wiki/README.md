This is our wiki.
The best way to use it is to clone and use folder wiki as an [obsidian](http://obsidian.md) vault (or link it into your existing vault)

**Start at the wiki** [index](PROJECTS/iC/wiki/index.md)

Every time something is pushed to main, GitLab CI is run, and a [webpage](https://icsystemsai.gitlab.io/wiki/) is built. Obsidian links should work there, however they do not work on gitlab.


It might happen that something breaks and the job fail, if you have issues, check:
https://gitlab.com/icsystemsai/wiki/-/jobs

# Publishing Obsidian.md notes with GitLab Pages
https://about.gitlab.com/blog/2022/03/15/publishing-obsidian-notes-with-gitlab-pages/


---
# Good Practices
* Try to add the responsible person to each note
* If you HAVE to include a media (image, etc...) Make sure it is as small as possible (at least optimized for web). 
* For drawings, we recommend using text-based formats like svg
* If you want to integrate this repo into your vault, instead of cloning it as a subdirectory, create a symlink to the `wiki/wiki` folder and you are golden
* Optionally check the note with Grammarly, language tool, or something similar.