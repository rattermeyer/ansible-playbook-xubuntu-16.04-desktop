# Git

This role installs git and some additional tools and installs a gitconfig file.

## Slightly longer explanation

If nothing else is specified, this role will install git, tig, meld, vim, gitk
and bash\_completion as additional packages. It also installs the [git bash prompt](https://github.com/magicmonty/bash-git-prompt).

It then starts configuring git with an opinionated gitconfig file.

This config file also includes a lot of useful git aliases.
These include most aliases presented by Nicola Paolucci in his [Blog](http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/).

I have left out several aliases, I am not using.

Beside these the following additional aliases have been added the following aliases:

### Handling Origin and Upstream Repositories
Because I am often contributing to Jekyll based blogs, I need to handle
upstream repositories.

I have added two alises for this `git clu` und `git pu`.
`git clu` is a git clone with upstream, which takes two arguments:

1. address for origin remote
2. address for upstream remote

The command clones the origin, sets the upstream address and fetches from upstream.

`git pu` is meant as a git pull upstream. This command fetches upstream and
merges upstream/master on the current branch.

### Log graphs
I have added some aliases as described by Slipp D. Thompson on (Stackoverflow)[http://stackoverflow.com/questions/1838873/visualizing-branch-topology-in-git/34467298#34467298], but changed
date display a bit.

## commits to be pushed
`git ctbps` will show the commits to be pushed to the origin corresponding branch.

## Role Variables

### List of mandatory variables
The following variables must be defined when using this role:

```yaml
git:
  user:
    account: richard
```
The given account will be used to install the gitconfig file.

And then a `config` variable must be set to point to a custom git configuration
that will be copied or you must specify

```yaml
git:
  user:
    name: Richard Attermeyer
    email: richard.attermeyer@gmail.com
```

See example playbooks.

### List of all variables

The variables below can all be overridden when calling this role.
As mentioned above, only very few are mandatory.

The packages_x11 are only installed if `gui_enabled` is set to `True`.
If `gui_enabled` is `True` the merge tool will be meld, otherwise vimdiff.

The git bash prompt version and theme can be customized using the
`git_bash_prompt` variables.

```yaml
---
# defaults file for git
home: "/home/{{git.user.account}}"
git_bash_prompt_version: "2.5.1"
git_bash_prompt_theme: Solarized
packages_nonx11:
  - git
  - tig
  - bash-completion
  - vim
packages_x11:
  - gitk
  - meld
gui_enabled: true
git_default:
  core:
    editor: vim
    autocrlf: input
  merge:
    tool: meld
  credential:
    helper: "cache --timeout=1800"
  color:
    ui: auto
    branch: auto
    diff: auto
    status: auto
  color_branch:
    current: red reverse
    local: blue
    remote: green
  color_diff:
    meta: yellow
    frag: magenta
    old: red bold
    new: green
    plain: white
  color_status:
    added: yellow
    changed: green
    untracked: cyan
  rerere:
    enabled: false
  rebase:
    autosquash: true
  filter_lfs:
    clean: "git-lfs clean %f"
    smudge: "git-lfs smudge %f"
    required: true
  push:
    default: simple
```

## Dependencies

Currently none.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  roles:
     - { role: username.rolename, x: 42 }
```

## License

BSD

## Author Information

Richard Attermeyer

- [Blog](http://www.rattermyer.de)
- [Github](https://github.com/rattermeyer)
- [Twitter](https://twitter.com/rattermeyer)
