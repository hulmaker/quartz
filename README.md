# Quartz v4

> “[One] who works with the door open gets all kinds of interruptions, but [they] also occasionally gets clues as to what the world is and what might be important.” — Richard Hamming

Quartz is a set of tools that helps you publish your [digital garden](https://jzhao.xyz/posts/networked-thought) and notes as a website for free.
Quartz v4 features a from-the-ground rewrite focusing on end-user extensibility and ease-of-use.

🔗 Read the documentation and get started: https://quartz.jzhao.xyz/

# Setup
 1. fork [jackyzha0/quartz](https://github.com/jackyzha0/quartz)
 2. Use the [ExplicitPublish](https://quartz.jzhao.xyz/plugins/ExplicitPublish) plugin, setup layout, etc...
 3. create a private repo for storing notes, connect it to your obsidian vault.
 4. Generate personal access token and set it as an action secret to the forked quartz repo
 5. setup [hosting](https://quartz.jzhao.xyz/hosting#github-pages) via GitHub pages
 7. change the build pipeline to pull submodules with using the PAT secret
 8. make sure the quartz uses the submodule as a content directory
 9. change the pipeline so that you can run it manually
 10. run everything and profit.
 11. update the submodule from time to time so that the build time is shorter.


# Publishing Changes
 1. Set metadata flag "publish: true" to all notes you want to publish.
 2. Push the changes to the private GitHub repo: [notes](https://github.com/hulmaker/notes)
 3. Go to the public [quartz](https://github.com/hulmaker/quartz/tree/v4) repository and run the GitHub action manually!
 4. Notes that were explicitly marked to be published should be available via: [https://hulmaker.github.io/quartz/](https://hulmaker.github.io/quartz/)
