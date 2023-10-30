# What is...?
Compl[ie]mentary *nix APIs on Windows/MinGW64.

## Raison d'être

MinGW64 headers are public domain, but lack certain features. We strive at (O officespeak!) patching the holes and glueing the gaps in their implementation of POSIX, BSD and Linux APIs — aiming (eventually) at a complete Linux userspace implementation buildable for and runnable under Windows RT and the later versions of Windows.

(Why RT? Check https://github.com/armdevvel — the front page of Project Rakko dedicated to returning Windows RT devices to useful life.)

## Composition

LibMoreGW is a metaproject. It contains no buildable code by itself; instead it provides a list of libraries (consumable via `pkg-config`) comprising the eventual product.
You can link with the libraries selectively based on the features you need. Also, if MinGW64 finally provides a first-class implementation of a certain API family, you are
covered — simply replace the affected `-lsomething` flag.

Component|Maturity|Origin|Linkage|Description
---|---|---|---
[libwusers](https://github.com/treeswift/libwusers)|RC|in-house|`-lwusers`|`<pwd.h>` and `<grp.h>` (user and group API)
[libfatctl](https://github.com/treeswift/libfatctl)|RC|in-house|`-lfatctl`|*nix file API (e.g. the`*at` function family)
[libmemmap](https://github.com/treeswift/libmemmap)|β|in-house|`-lmemmap`|`<sys/mman.h>` virtual memory API
[silverware](https://github.com/treeswift/silverware)|early|in-house|`-lsilver`|*nix process API
[glob](https://github.com/treeswift/glob)|RC|3rdparty|-lglob|`glob()` and `fnmatch()` API
[getline](https://github.com/treeswift/getline-compatible)|β|3rdparty|`-lgetline`|`getline` API (a very basic implementation)
[libob](https://github.com/treeswift/strptime)|RC|3rdparty|`-lstrptime` or `-lob`|the `strptime` function (highly configurable)

# Legal

Components we maintain ourselves are released into the [public domain](https://en.wikipedia.org/wiki/Public_domain) with a no-strings-attached [Unlicense License](LICENSE).

Components we have selected as useful third-party building bricks are released either [under a permissive license](https://en.wikipedia.org/wiki/Permissive_software_license) — such as BSD, Apache, MIT or CC-A — or right into the [public domain](https://en.wikipedia.org/wiki/Public_domain).

## Why?

While being entirely pro-free market, we don't believe in appropriation of ideas, and software is nothing but ideas.

We obey the copyright law because we don't think it's the right time for a publicly announced disobedience campaign, and for many other purely opportunisic reasons. However,
when it comes to the status our own work, there is nothing at stake but our principles, and our principles are stated above: ideas are nothing but similarities, and there is
nothing in pure similarity that has anything in common with any form or property recognized by common law. In certain theistic philosophies, ideas are created by God. In the
materialistic philosophy, there is simply no such thing; ideas are properites of matter (something that exists) — nothing more than _likenesses_ among something that exists.
One can own a red scarf, a red dress, a red hat, a red car or a red Japanese maple tree — etc., etc. All of them can be put under a lock or behind a fence, leased,
subleased, donated or trashed; but one can't own the red _color_. You can have three cars, three laptops, three homes, three passports of different countries — but you can't
own _the number three_, or any number, for that matter — and the digital representation of software is nothing but _numbers_.
*In a nutshell, there is no reasonable philosophy behind the copyright law — and can't be any.*

If you think that a conceptually unsound law is still worth enactment and enforcement on the grounds of the social benefits it brings, you might as well defend establishment
of a government-endorsed religion on those same grounds. We don't.

A legislated belief in the real existence of ideas, and in human _creation_ of ideas, is nothing better than a legislated belief in God.

# Extending LibMoreGW

If you'd like to 
* file a "missing feature" request;
* propose a component for inclusion into `libmoregw` —

GitHub provides the necessary tools. File an issue here: https://github.com/treeswift/libmoregw

The three primary criteria for adoption of a certain component are
* the existence of actual POSIX/BSD/Linux/some*nix API it provides *used within a real software project you are developing or porting*;
* the _breadth_ of the component (i.e. whether it "does one thing and does it well");
* permissive license (see above).

