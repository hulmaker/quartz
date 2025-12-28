---
tags:
  - on/dev
  - type/tutorial
link: https://github.com/jackyzha0/quartz
publish: true
---
[Quartz](https://github.com/jackyzha0/quartz) is a set of tools that helps you publish your [digital garden](https://jzhao.xyz/posts/networked-thought) and notes as a website for free. Here is a guide on how I did it.

# Setup
1. fork [jackyzha0/quartz](https://github.com/jackyzha0/quartz)
2. Use the [ExplicitPublish](https://quartz.jzhao.xyz/plugins/ExplicitPublish) plugin, setup layout, etc...
3. Create a private repo for storing notes, connect it to your obsidian vault.
4. Integrate the private repo to quartz as a git submodule.
5. Generate personal access token and set it as an action secret to the forked quartz repo.
6. Setup [hosting](https://quartz.jzhao.xyz/hosting#github-pages) via GitHub pages.
7. Change the build pipeline to pull submodules with using the PAT secret
8. Make sure the quartz uses the submodule as a content directory
9. Change the pipeline so that you can run it manually
10. Run everything and profit.
11. Update the submodule from time to time so that the build time is shorter.

# Publishing Changes
1. Set metadata flag "publish: true" to all notes you want to publish. (like in this note)
2. Push the changes to the private GitHub repo: [notes](https://github.com/hulmaker/notes)
3. Go to the public [quartz](https://github.com/hulmaker/quartz/tree/v4) repository and run the GitHub action manually!
4. Notes that were explicitly marked to be published should be available via: [https://hulmaker.github.io/quartz/](https://hulmaker.github.io/quartz/)