---
layout: post
status: publish
published: true
title: Maintaining Your Sanity in a Large Slack Instance
author:
  display_name: John Koerner
  login: admin
  email: blog@johnkoerner.net
  url: ''
author_email: blog@johnkoerner.net
categories:
- tools
tags:
- slack
---
If you have ever worked in a large Slack instance, you know some of the pains that come along with it. The random `@here` or `@channel` and the subsequent responses admonishing the people for alerting 6000 of their closest friends. The pinging from channels that you only slightly care about. The people who forget that the chat instance is still a professional setting.

In our Slack instance, `@here` and `@channel` are enabled.  They are useful in small channels, if used judiciously. Unfortunately, they cause a ruckus in larger channels, but people tend to learn pretty quickly not to abuse them.  In my opinion this is an area where Slack can improve, by only allowing channel owners the ability to use `@here` and `@channel`.  The could also provide another keyword that allows people to target the owners of a channel such as a `@owners` keyword. 

In the two years or so that I have been working in a large Slack instance, I have learned a few things and thought I would share.  Here are a few of my best practices when working with slack.

## Organize Your Channels

Channels will fall into one of a few categories:

#### *Lifeblood Channels*
These channels are the channels you live in day in and day out. You want to know immediately when someone posts in these channels. A good post here will make your day, a bad post here could ruin a weekend. 

#### *Informational Channels*
These channels provide useful information to you and when you get some time, you will catch up on the channel and you may chime in from time to time. You joined this channel because you have a vested interest in the topic at hand, but it may not affect your day to day work.

#### *Corporate Channels*
These channels are used by various levels of management to share information.  They tend to have surges of information and then a lot of downtime. Usually this is required reading, but can be done at your leisure.

#### *The Required Channel*
You can't leave this channel.  Hopefully you have good admins that lock down who can post here. This is hopefully just a Corporate Channel you cannot leave.

#### *The ignored channels*
These channels have nothing to do with your job and, depending on the size of your slack instance, you may not even know they exist.

---

Once you've decided what category applies to a given channel you can then customize how that channel is displayed to you.  Your lifeblood channels should be favorited by clicking the star in the top left corner of the channel. You can also star any direct message conversations you have with colleagues that you work with on a daily basis.

With your lifeblood channels and colleagues starred, you can now configure slack to always display those channels on the sidebar and hide all others. Under preferences, go to the sidebar options and select the `My Unreads, along with everything I've starred` option:

![Sidebar Preferences Screenshot](/content/SidebarPrefs.png)

All other channels will only display when there is new content in those channels.  For those required, corporate, or information channels where there are a lot of posts, but only mildly useful content, you can mute those channels, to prevent extra alerts from appearing on your slack client.

![Mute Channel](/content/MuteChannel.png)

Muting a channel will prevent it from appearing unread, but you may still get badges by the channel for `@here` or `@channel` messages. For channels where `@here/@channel` get annoying, you can even mute those alerts in the channel notification preferences:

![Mute Here](/content/MuteHere.png)

You can even star a channel you have muted, so it will appear in your list at all times, but you will never receive a notification from the channel. This is useful for those chatty channels that you just want to check in with from time to time.

## Manage Your Alerts
If you don't setup your alerts properly in Slack, your UI will be a mishmash of channels with various numbers by them and a whole bunch of bolded channels which you have joined over the course of doing business. 

My recommendation is to only configure notifications for `Direct Message, mentions & keywords`. Again, this is under your preferences in the notifications section:

![Notifications Screenshot](/content/Notifications.png)

#### *Keywords*
Keywords are an awesome feature of Slack that provide notifications based on keywords. You can configure keywords to keep you abreast of others talking about your feature or product across your company.  Any channel to which you belong where a keyword is mentioned will result in a notification. This is managed under the notifications section of your slack preferences.

![Slack Keywords](/content/SlackKeywords.png)

---
Slack is a very useful tool, but it can get unwieldy fast. Using the settings I outlined above, your large slack instance will be more productive and less of a distraction.

Do you have a tip for making Slack more productive or less of a distraction?  If so, share it below.  