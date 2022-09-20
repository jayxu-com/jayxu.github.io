---
id: 16842
title: 'How Time Machine Works its Magic [zz]'
date: '2019-07-25T17:06:30+08:00'
author: Jay
excerpt: 'There are two main bits of "Magic" behind Time Machine, explained below'
layout: post
guid: 'https://www.jayxu.com/?p=16842'
permalink: /2019/07/25/16842
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '1300'
image: 'https://d1k8eqsfs47rrv.cloudfront.net/log/wp-content/uploads/2019/07/Time-Machine-screen-800x450.jpg'
---

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>Original: <a href="https://www.baligu.com/pondini/TM/Works.html">https://www.baligu.com/pondini/TM/Works.html</a></p></blockquote>
<!-- /wp:quote -->

<!-- wp:image {"id":16845,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://www.jayxu.com/log/wp-content/uploads/2019/07/Time-Machine-screen-800x450.jpg"><img src="https://www.jayxu.com/log/wp-content/uploads/2019/07/Time-Machine-screen-800x450.jpg" alt="" class="wp-image-16845"/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>There are two main bits of "Magic" behind Time Machine, explained below:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>The&nbsp;<strong><em>File System Event Store --</em></strong>&nbsp;How changes are found quickly (<strong>blue</strong>&nbsp;box)<br></li><li><strong><em>Hard Links&nbsp;</em></strong>-- How "incremental" backups are, in effect, full backups (<strong>tan</strong>&nbsp;box)</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>And some other, more technical, stuff, on separate pages:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://www.baligu.com/pondini/TM/Works1.html">Backup Structure</a></li><li><a href="https://www.baligu.com/pondini/TM/Works2.html">How Local Backups are Stored</a></li><li><a href="https://www.baligu.com/pondini/TM/Works3.html">How Network Backups are Stored in Sparse Bundles</a></li><li><a href="https://www.baligu.com/pondini/TM/Works4.html">Inclusion and Exclusion handling and the Preferences file</a></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph {"dropCap":true,"backgroundColor":"pale-cyan-blue"} -->
<p class="has-background has-drop-cap has-pale-cyan-blue-background-color">The&nbsp;<strong><em>File System Event Store</em></strong>&nbsp; is a hidden log that OSX keeps on each HFS+ formatted disk/partition of changes made to the data on it.&nbsp;&nbsp; It doesn’t list every&nbsp;<em>file</em>&nbsp;that’s changed, but each&nbsp;<em>directory</em>&nbsp;(folder) that’s had anything changed inside it.&nbsp; That saves lots of space in the log, since often there are multiple changes to the same folder.&nbsp; Each such change is called an&nbsp;<em>event.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-cyan-blue"} -->
<p class="has-background has-pale-cyan-blue-background-color">Any process can use it to find what’s been changed since the last&nbsp;<em>event&nbsp;</em>that process handled.&nbsp; That’s how&nbsp;<em>Spotlight</em>, for example, knows when a file has been added or changed and needs to be re-indexed.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-cyan-blue"} -->
<p class="has-background has-pale-cyan-blue-background-color">Normally, Time Machine can use it to find out what’s changed and needs to be backed-up, since it’s far faster than comparing everything on your system to the backups, as some other backup apps do.&nbsp; (And it’s the reason that Time Machine can’t back up disks with other formats.)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-cyan-blue"} -->
<p class="has-background has-pale-cyan-blue-background-color">But OSX can’t keep the log forever, of course, so if you haven’t done a backup in a long time, or there’s been a very large volume of changes (such as installing an OSX upgrade, which will add or change tens of thousands of files), the database won’t be complete.&nbsp; Or, if your system shuts down abnormally, such as from a software problem, power loss, or forced power-off, it will also be suspect.&nbsp; OSX will replace the&nbsp;<em>Event Store</em>&nbsp;and assign a new "UUID" to it (and send a message to that effect to your logs).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-cyan-blue"} -->
<p class="has-background has-pale-cyan-blue-background-color">When that happens, the next backup will log a message about an "Event store UUID" not matching, meaning it's not the same one as on the previous backup.&nbsp;&nbsp; Then Time Machine has to do a "deep scan" ("deep traversal" on Snow Leopard or Leopard), comparing everything on your system to the backups.&nbsp; If you see a long "Preparing" phase ("Calculating changes" on Snow Leopard), that’s what’s going on.&nbsp;&nbsp; From 10.6.3 through 10.6.8, you’ll see&nbsp;<em>Scanning nnnn files</em>&nbsp;messages on the TM Preferences Window and the TM Menu display from your menubar.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-cyan-blue"} -->
<p class="has-background has-pale-cyan-blue-background-color">The time required for this depends on a number of things, but mainly the number of files on your system (more than the total size), and the type of connection to your backups.&nbsp; So a relatively small system using a FireWire800 external drive will be far faster than a larger system being backed-up wirelessly to a Time Capsule.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"dropCap":true,"backgroundColor":"pale-pink"} -->
<p class="has-background has-drop-cap has-pale-pink-background-color"><strong><em>Hard Links</em></strong>&nbsp; act a bit like&nbsp;<em>aliases</em>, but much more efficiently, and are the key to how Time Machine can back up only what’s changed, but have each backup be, in effect, a full backup of everything that was on your system at the time.&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">When Time makes your first backup, it copies everything (except some system work files, trash, etc).&nbsp; It also makes a dated&nbsp;backup folder, and places hard links in it to all the backup copies it just made.&nbsp; Then when Time Machine makes a second backup, it copies everything that changed since the first backup, makes another dated backup folder, and puts hard links in it to the new backup items.&nbsp; So far, so good.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">But here’s the trick:&nbsp; it&nbsp;also&nbsp;puts hard links in the second backup folder to the items that&nbsp;didn’t&nbsp;change.&nbsp; So the folder now contains links to&nbsp;<strong><em>everything</em></strong>&nbsp;that was on your system at the time of the second backup.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">This is greatly oversimplified, but should illustrate how it works:&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Create File A and File B, and run an initial backup (backup folder #1 below).&nbsp;</li><li>Then delete File A, create file C, and run another (backup folder #2 below).</li><li>If you look at the<strong>&nbsp;backup folders&nbsp;</strong>via the Finder, you’ll see a bit of an illusion:</li></ul>
<!-- /wp:list -->

<!-- wp:image {"id":16843,"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="https://www.jayxu.com/log/wp-content/uploads/2019/07/shapeimage_1.png"><img src="https://www.jayxu.com/log/wp-content/uploads/2019/07/shapeimage_1.png" alt="" class="wp-image-16843"/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">It&nbsp;appears&nbsp;there are two copies of File B, but there aren’t;&nbsp; each&nbsp;<strong>Backup Folder</strong>&nbsp;contains a hard link to a single copy of File B.&nbsp;&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">This also explains how, when it’s out of space, Time Machine can delete your first backup, but all the other backups are still full versions of your system:&nbsp;&nbsp; the trick is, the&nbsp;backup folder and all its hard links are deleted, but the actual&nbsp;backup copies&nbsp;aren’t deleted if there are&nbsp;any&nbsp;remaining hard links to them.&nbsp; If Backup Folder #1 is deleted, the backup copies of files B and C remain (and you regain only the space used by File A on your backup drive).</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>A little "twist" to this is, if you add-up the sizes of the two <strong>Backup Folders</strong>, you’ll count File B twice!   This is because, unlike a "normal" file system, the backup copies don’t "belong" to one particular backup folder -- they're in both folders <strong>at the same time.</strong>   That's why you'll get odd figures from the Finder and/or 3rd-party utilities -- sometimes the <strong>Backups.backupdb</strong> folder is much less than the total of the backup folders;  other times it will be shown as the <strong>sum</strong> of them, possibly much larger than the backup drive!</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">Now you’re probably thinking, there must be about a zillion of those hard link thingies in every backup folder, taking forever to create and delete.&nbsp; But Time Machine has yet another trick up it’s sleeve:&nbsp; If nothing in a folder is changed, Time Machine makes a&nbsp;single&nbsp;hard link for the&nbsp;folder, not one for each file inside it.&nbsp; This is especially slick when you think about your system folders:&nbsp; they contain tens of thousands of folders and sub-folders several levels deep, that rarely change.&nbsp; So instead of making a&nbsp;<em>couple of hundred thousand</em>&nbsp;links for every backup, there are often only a few.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"backgroundColor":"pale-pink"} -->
<p class="has-background has-pale-pink-background-color">In fact, the OSX File System was&nbsp;<em>changed</em>&nbsp;effective with Leopard to allow these "directory-level" hard links, so Time Machine would work.&nbsp; That’s one of the reasons why Tiger and earlier versions of OSX (not to mention other operating systems) are&nbsp;<strong>mystified</strong>&nbsp;by Time Machine backups.&nbsp; They cannot make any sense of the links that look like folders.</p>
<!-- /wp:paragraph -->