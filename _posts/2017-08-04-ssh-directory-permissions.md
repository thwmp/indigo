---
title: "ssh setup and configuration"
layout: post
date: 2017-08-04 19:18
image: /assets/images/markdown.jpg
headerImage: false
tag:
- ssh
- linux
category: blog
author: John Amori
description: ssh file permission mishaps
# jemoji: '<img class="emoji" title=":ramen:" alt=":ramen:" src="https://assets.github.com/images/icons/emoji/unicode/1f35c.png" height="20" width="20" align="absmiddle">'
---

## Summary:

 Working with ssh can be annoying at times, copying keys around and debugging access issues with public-key authentication.
 I recently came across a face-palm moment when my .ssh directory had write permissions for the group. 
 
Despite previous experience, I was still fumbled by why my configuraiton wasn't working. My /etc/ssh/sshd_config had all the correct settings. This simple mistake unforunately lead to making extra keys, double checking confiugration and restarting the service more than needed and checking logs.
 
 Thanks to some savior at [StackExchange](https://unix.stackexchange.com/questions/351847/ssh-public-key-not-working-for-specific-user) I realized the error.
 
 I don't plan to go into detail on how ssh keys work or how to configure your server to use them, there are enough resources available already. You'll get so much more out of reading the man pages and learing to really utilize the whole suite of tools that ssh has to offer. I'm using this blog as more of a bookmarking tool. 
 
---
 
 ## My Notes:
 
 * ~/.ssh should have 700 permissions
 * authorized_keys 600 permissions
 * auth logs found in /var/log/auth.log
 * configuration settings in /etc/sshd/sshd_config
 * restart the service after any changes are made
 * When working with a lot of hosts, setting up a ~/.ssh/config file is key (see atlassian link below)
 * It's easy to copy an ssh key to a remote host with:
 
 ssh-copy-id -i ~/.ssh/rsa_id.pub username@hostname

---
 ## Links:
 
 * <https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/>
 * <https://confluence.atlassian.com/bitbucket/configure-multiple-ssh-identities-for-gitbash-mac-osx-linux-271943168.html>
 * <https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server>

 
 
