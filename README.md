# MZD's shell profile

It's how I like it, your mileage may vary.

Mostly, this is a collection of bash functions I have accreted. 

Specific install steps at end of this document.

## Alias Definitions

To keep order in my shell aliases, I wanted to put them in discrete files. So, the `.rcd` directory is meant to just hold includes to be sourced by `.bashrc`/`.zshrc`.

```bash

#
# Auto-load shell resource files from .rcd
if [ -d ~/.rcd ]; then
	for f in ~/.rcd/*
	do
		if [ -f "$f" ]; then
			. "$f"
		fi
	done
fi
```

If you add the above to your `...rc` file, you will get most of the benefits of this repo.

## Custom Prompt

Just for fun, I define a custom prompt. There are some other examples commented-out in `.bashrc`, so play with it.

See the `PS1=` definitions.

## Crypto

#### SSH-keys

This file contains utils motivated by the need to ease working with ssh keys based on fingerprints.

use the source, Luke.

#### GPG-Keys

A little guidance for basic GPG key operations. Especially, clearly getting Key ID's and Fingerprints since the regular output doesn't make ID's clear. Required arguments are passed via env, and validation will tell you what is missing. 

Most functions are prefixed with `gpg-`, so you can discover them with completion. One exception is `git-configure-signing()` which is just a friendly wrapper around `git config --global` to set your signing-key.

## SSH

This is just my SSH config file, but the configs in the beginning may be of general interest.

## Git Config

Use the configure-git.sh script to set git global configs with prompts and defaults that I like.

It will recommend and point you to the functions to configure commit signing (create a key, and update your global config).

## Setup

I have not tried deploying the `.bashrc` file contents to Zsh, let me know how it goes! 

Clone this repo to `~/.dot-profile` (or whatever you want).

Not every step is required. In your `~` dir...

```bash

# install aliases and custom prompt
 $> ln -s .dot-profile/.rcd
 $> ln -s .dot-profile/.bashrc

# use ssh config
 $> ln -s .dot-profile/ssh_config ~/.ssh/config

# configure git with prompts
 $> .dot-profile/configure-git.sh

# generate a new signing key
 $> gpg-generate-signing-key USER_NAME='Tenex Dev' EMAIL=you@domain.com

# get the new key ID
 $> gpg-list-key-ids

# enable signed commits
 $> configure-git-signing KEY_ID=<the-key-id> 
```