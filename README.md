# Mac Bootstrap

## ⚠️ This project is no longer maintained.

Mac Bootstrap was a fun project that ran for several years. In the end, the maintenance became too much, and I began looking for simpler solutions. I've recently completed a [major overhaul of my dotfiles](https://github.com/joshukraine/dotfiles/pull/64), also with simplicity and easier maintenance in mind. The README there presents my new approach for bootstrapping a Mac computer based on [my fork of Laptop][joshuas-laptop] + my dotfiles.

&#9657; [Check it out](https://github.com/joshukraine/dotfiles/blob/master/README.md)

---

![mac-bootstrap screenshot][screenshot]

This script will provision a new machine running a fresh install of [macOS Catalina (10.15)][catalina]. It installs and configures the software, dotfiles, and general preferences I use for web development — primarily [Rails][rails], [React][react], and [Vue][vue]. The command line environment is based on [Fish][fish] (or [Zsh][zsh]), [Neovim][neovim], and [Tmux][tmux] running in [iTerm2][iterm2] or [Alacritty][alacritty].

The [`bootstrap`][bootstrap] script is very specific to the Mac platform. Version 5.x has been successfully tested on the following versions of macOS:

* Catalina (10.15)

Previous versions of Mac Bootstrap have been successfully tested on the following versions of macOS:

* Mojave (10.14)
* High Sierra (10.13)
* Sierra (10.12)
* El Capitan (10.11)

&#9657; **Looking for dotfiles only? Check out [My Dotfiles for macOS](http://jsua.co/dotfiles)**

## Prerequisites

1. Make sure your software is up to date:

        sudo softwareupdate -i -a --restart

1. Install Apple's command line tools:

        xcode-select --install

1. Reboot, check for additional updates, then reinstall and reboot as needed.

## Installation

To install with a one-liner, run this:

```sh
curl --remote-name https://raw.githubusercontent.com/joshukraine/mac-bootstrap/master/bootstrap && sh bootstrap 2>&1 | tee ~/bootstrap.log
```

Want to read through the script first?
```sh
curl --remote-name https://raw.githubusercontent.com/joshukraine/mac-bootstrap/master/bootstrap
less bootstrap
sh bootstrap 2>&1 | tee ~/bootstrap.log
```

WARNING: This script will ask for your sudo password multiple times. You'll need to babysit it for a while. 😉

## What does it do?

When you invoke `bootstrap`, here's what it does:

* Step 1: Run my adaptation of thoughtbot's [Laptop script][laptop]. This is a provisioning script which installs lots of goodies like Homebrew, asdf, postgres, etc. My version is now stored locally in this repo under [`install/laptop`][my-laptop]. Step 1 also installs a variety of packages via [Homebrew Bundle][brew-bundle].
* Step 2: Install [Oh My Zsh][omz] if Zsh selected as default shell.
* Step 3: Set a variety of [macOS defaults][macos-defaults]. (adapted from [https://mths.be/macos][mths])
* Step 4: Install various [executable scripts][exe-scripts] (mostly for Tmux and Git) to `$HOME/bin`.
* Step 5: Set up a default [Tmuxinator][tmuxinator] profile for managing tmux sessions.
* Step 6: Install [Ukrainian spell-check dictionaries][dictionaries].
* Step 7: Clone [My Dotfiles for macOS][dotfiles] and symlink them to `$HOME` or `$XDG_CONFIG_HOME` as needed.

NOTE: Previously, I used the `bootstrap` script to set up many of the standard directories I use in my work. But since I now have [Dropbox Plus][db-plus], all those directories are downloaded automatically after Dropbox is installed. Once they've synced, I symlink them into place in `$HOME`.

## Post-install Tasks

After running `bootstrap` there are still a few things that need to be done.

* Restart your machine in order for some changes to take effect.
* Complete [post-install tasks][post-install-tasks] from dotfiles README.
* Set up desired macOS keyboard shortcuts (see list below)

## macOS Keyboard Shortcuts

These are my (current) primary macOS keyboard shortcuts:

* Alfred: &#8984;Space
* Clipboard (Alfred) &#8997;&#8984;C
* Spotlight search: &#8984;&#8679;Space
* Switch input source: &#8963;&#8679;Space
* Fantastical: &#8997;&#8984;Space
* iTerm2 hotkey window: &#8997;Space
* Remap Caps Lock to CTRL (anyone know a way to automate this?)

## How to personalize Mac Bootstrap for your own use.

No one else's development setup will ever be a perfect match for you. That said, if your needs are close enough to mine, you might benefit from using the same shell scripts and overall structure, and just swapping out the particulars with your own. Here's my recommended approach to doing that:

1) Fork this repo and clone your new fork to your local machine.

2) Review the `VARIABLE DECLARATIONS` section and customize as desired.

3) Review the 7 steps in [`bootstrap`][bootstrap] and make your own customizations. Here's an overview of what's going on:

* Step 1 (required): Take a look at [Laptop][laptop] and see what you might want to tweak. One of the biggest things to review is the `brew bundle` list of packages and casks that will be installed. Customize as needed. Laptop also sets up some basics that are required by the bootstrap script later on.
* Step 2 (recommended): Use Oh My Zsh?
* Step 3 (required): Review general macOS settings in `install/macos-defaults` and adjust as needed. This script also sets things like `HostName` which are needed later for the dotfiles installation.
* Step 4 (recommended): Install scripts to `~/bin`?
* Step 5 (recommended): Set up Tmuxinator profile?
* Step 6 (optional): Install Ukrainian language utilities? Maybe you're interested in some [other language extensions][lang-extensions]?
* Step 7 (required): The dotfiles. Update the `$DOTFILES_*` variables (see [`bootstrap`][bootstrap] under "VARIABLE DECLARATIONS") to reference your dotfiles. As a starting point, you can [fork mine][dotfiles] and then point to your fork.

4) Create `~/dotfiles/local/config.fish.local` or `~/.zshrc.local`, `~/.gitconfig.local`, and `~/.vimrc.local` and add in your personal information. These files are sourced in `~/.config/fish/config.fish` or `~/.zshrc`, `~/.gitconfig`, and `~/.vimrc`  respectively.

5) Update the README with your own info, instructions/reminders so you don't forget what you did, and especially the correct install URL:

```sh
curl --remote-name https://raw.githubusercontent.com/YOUR-GITHUB-USERNAME/mac-bootstrap/master/bootstrap && sh bootstrap 2>&1 | tee ~/boostrap.log
```

6) Run the script on your machine and wait for the first error. 😇 Then fix, commit, push, and repeat.

## Some of my favorite dotfile repos

* Pro Vim (https://github.com/Integralist/ProVim)
* Trevor Brown (https://github.com/Stratus3D/dotfiles)
* Chris Toomey (https://github.com/christoomey/dotfiles)
* thoughtbot (https://github.com/thoughtbot/dotfiles)
* Lars Kappert (https://github.com/webpro/dotfiles)
* Ryan Bates (https://github.com/ryanb/dotfiles)
* Ben Orenstein (https://github.com/r00k/dotfiles)
* Joshua Clayton (https://github.com/joshuaclayton/dotfiles)
* Drew Neil (https://github.com/nelstrom/dotfiles)
* Kevin Suttle (https://github.com/kevinSuttle/OSXDefaults)
* Carlos Becker (https://github.com/caarlos0/dotfiles)
* Zach Holman (https://github.com/holman/dotfiles/)
* Mathias Bynens (https://github.com/mathiasbynens/dotfiles/)
* Paul Irish (https://github.com/paulirish/dotfiles)

## Helpful web resources on dotfiles, et al.

* http://dotfiles.github.io/
* https://medium.com/@webprolific/getting-started-with-dotfiles-43c3602fd789
* http://code.tutsplus.com/tutorials/setting-up-a-mac-dev-machine-from-zero-to-hero-with-dotfiles--net-35449
* https://github.com/webpro/awesome-dotfiles
* http://blog.smalleycreative.com/tutorials/using-git-and-github-to-manage-your-dotfiles/
* http://carlosbecker.com/posts/first-steps-with-mac-os-x-as-a-developer/
* https://mattstauffer.co/blog/setting-up-a-new-os-x-development-machine-part-1-core-files-and-custom-shell

## License

Copyright &copy; 2020 Joshua Steele. [MIT License](https://github.com/joshukraine/mac-bootstrap/blob/master/LICENSE)

[alacritty]: https://github.com/alacritty/alacritty
[bootstrap]: https://github.com/joshukraine/mac-bootstrap/blob/master/bootstrap
[brew-bundle]: https://github.com/Homebrew/homebrew-bundle#usage
[catalina]: https://www.apple.com/macos/catalina/
[db-plus]: https://db.tt/Kmoif6SG
[dictionaries]: https://extensions.openoffice.org/en/project/ukrainian-dictionary
[dotfiles]: http://jsua.co/dotfiles
[exe-scripts]: https://github.com/joshukraine/mac-bootstrap/tree/master/bin
[fish]: http://fishshell.com/
[iterm2]: https://www.iterm2.com/
[lang-extensions]: http://extensions.services.openoffice.org/en/search?f[0]=field_project_tags%3A157
[laptop]: https://github.com/thoughtbot/laptop
[macos-defaults]: https://github.com/joshukraine/mac-bootstrap/blob/master/install/macos-defaults
[mths]: https://mths.be/macos
[my-laptop]: https://github.com/joshukraine/mac-bootstrap/blob/master/install/laptop
[joshuas-laptop]: https://github.com/joshukraine/laptop
[neovim]: https://neovim.io/
[omz]: http://ohmyz.sh/
[post-install-tasks]: https://github.com/joshukraine/dotfiles#post-install-tasks
[rails]: https://rubyonrails.org/
[react]: https://reactjs.org/
[screenshot]: https://res.cloudinary.com/dnkvsijzu/image/upload/v1584124959/screenshots/mac-bootstrap-mar-2020_pmadrx.png
[stratus3d]: http://stratus3d.com/blog/2015/02/28/sync-iterm2-profile-with-dotfiles-repository/
[tmux]: https://github.com/tmux/tmux/wiki
[tmuxinator]: https://github.com/tmuxinator/tmuxinator
[vue]: https://vuejs.org/
[zsh]: https://www.zsh.org/
