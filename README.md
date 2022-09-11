# Oryon's Journal
> The captains logbook

Personal &amp; Technical Notes and Documentations

- [Agile Principles](agile-principles.md)
- [Interesting Blogposts](interesting-blogposts.md)
- [Link Library](link-library.md)

Tutorials on several Topics  


# Cloning the 'secret-journal' for obsidian -> inlcude public files (this 'public journal')

    git clone --recurse-submodules https://github.com/oryon-dominik/secret-journal

    # has been achieved by adding this repo as a submodule to secret-journal
    git submodule add https://github.com/oryon-dominik/journal public
    git submodule set-branch --branch trunk public
