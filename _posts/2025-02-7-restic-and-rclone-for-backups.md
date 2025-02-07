---
layout: post
title:  "Using Restic for Easy Backups When You Can't Avoid OneDrive"
tags: backup cli-tools onedrive microsoft restic
---

In your working life, it is a sad truth that you can't always use the technologies you might prefer.
Policies and decisions can be made at varying levels of your organisation that dictate and restrict your use of tools.
In most organisations, this means interacting with software and products developed by Microsoft,
and if you use a Linux distribution for your OS,
this will invariably lead to compatibility issues and interfacing pain.
I want to share one technological solution that has eased the pain of doing this for the particular case of creating backups.

## Backup Storage Location

I'm not going to justify the necessity of keeping *full* backups of your machine because that is covered extensively by many sources.
If you have ever lost a significant amount of data from a piece of hardware giving up the ghost or a software update gone awry,
then you know through difficult experience the truth of the previous statement.
What I instead want to address here is the problem of where to store your backups once you have decided to make them.

For my personal laptop, I use an external hard drive, but in a work context this often isn't appropriate for what I suppose is mainly security  issues:
having a slew of hard drives floating around with potentially sensitive data on them is just asking for trouble.
If your company has a Microsoft 365 subscription, then it is likely the policy will be for any off-device storage to be on that.
This is already done by default for Windows users,
but returning to the observations in the first paragraph,
how does someone on a Linux machine get their backups onto OneDrive?

## How to Create Your Backup

I grappled with this question for quite an extended period.
One option I used for a while was use the tried-and-trusted `tar` to create compressed archives of my home folder,
and then I would upload those via the browser interface to OneDrive.
However, this very quickly grows the storage size for all your backups,
and it is wasteful because there is realistically quite a lot of duplication between backups.
`tar` can mitigate this with incremental archive creation,
but this is fundamentally quite fiddly and hard to implement yourself.
However, the real problem I was encountering was that the archive had to initially be created *somewhere* on my devices hard drive,
meaning it no longer becomes possible to do once your hard drive is more than half full.

Luckily, I finally happened upon an amazing CLI tool called [`rclone`][rclone],
which eventually led me to the related [`restic`][restic] for performing backups.
I had a false start with `rclone` because I thought I could just pipe my old `tar`-based backup through it and into OneDrive.
However, I quickly ran into issues with the connection being throttled or dropped,
and this seems to be something related to how OneDrive operates when something attempts to upload a massive file to it.
It is `restic` that nicely wraps `rclone` and handles appropriate chunking of the data being backed up so that this problem is avoided.

## Configuring Restic

First, you will need to initialise what `restic` calls a "repository" where it will store your backups.
The repository will be accessed through `rclone`, so you need to configure that first to authenticate with your storage provider,
in this case OneDrive.
[The instructions][restic-with-rclone] for using `restic` with `rclone` are very good and you can use that to get set up,
in particular making sure you navigate to the [`rclone` configuration step with OneDrive](https://rclone.org/onedrive/).
For the `rclone` configuration, you will set up a remote that has a `<name>`.
Remember that name because you will need to use it when specifying the `--repo` given to any `restic` command.

Once configured, I use the following command to perform the backup of my home folder:

```bash
restic --repo rclone:<name>:<backup-path> --verbose --exclude-file $HOME/configs/rclone_exclude backup ~/
```

Again, the `--repo` argument should include the `<name>` of the `rclone` remote you have configured,
and the `<backup-path>` will be the folder on OneDrive into which your backups will be stored.
Don't expect to see normal files in that folder, however.
`restic` does what most proper backup solutions do, which is store blobs with a hashed name.
There is then an index that helps instruct `restic` how these hashes can be used to recreate the file structure should you need to restore from the backup.
The other main option I provide is the `--exclude-file`, which specifies the folders or files in my home folder that I do not want backed up.
This is generally caches and temporary files that don't need backing up,
but there also isn't much harm in including them.
If you want a list to start from, [this is the exclude list I use](https://github.com/bielsnohr/configs/blob/master/rclone_exclude).
The file matching is according to [these patterns used by `rclone`](https://rclone.org/filtering/#patterns)

What impressed me with `restic` is that after the fairly straightforward configuration steps above it just worked.
There seem to be a set of sane defaults that will work in most cases and ensure your backup smoothly makes its way onto OneDrive.

[rclone]: https://rclone.org/
[restic]: https://restic.net/
[restic-with-rclone]: https://restic.readthedocs.io/en/stable/030_preparing_a_new_repo.html#other-services-via-rclone
