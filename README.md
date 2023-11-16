# What is...?
Compl[ie]mentary *nix APIs on Windows/MinGW64.

## Raison d'être

MinGW64 headers are public domain, but lack certain features. We strive at (O officespeak!) patching the holes and glueing the gaps in their implementation of POSIX, BSD and Linux APIs — aiming (eventually) at a complete Linux userspace implementation buildable for and runnable under Windows RT and the later versions of Windows.

(Why RT? Check https://github.com/armdevvel — the front page of Project Rakko dedicated to returning Windows RT devices to useful life.)

Our goal is to provide "organic" *nix-on-Windows coding experience, defined as follows: concepts of the *nix world that have a semantic and/or syntactic equivalents on
Windows (as per UCRT/MSVCRT or MinGW[64] CRT) *should stay equivalent*. Certain solutions, for example, introduce their own file descriptor (`fd`) table distinct from the
"real" table in the CRT, and have to substitute all public APIs accepting `fd`s with macros. This is a "walled garden" approach — or, more appropriately called, a "finger
in the dam" approach; it's unsustainable. If you roll out an API implementation that issues or accepts a file descriptor, it should be interoperable with the rest of the
standard API working with file descriptors. This is what we guarantee: no global redefinition of syntax or semantic.

The modern Windows OS is getting surprisingly close to its *nix roots, with entire *nix-only concepts (such as named sockets) becoming first-class on Windows. It's a trend
we welcome; but it's also a trend we find joy in keeping a little bit ahead of.

## Composition

LibMoreGW is a metaproject. It contains no buildable code by itself; instead it provides a list of libraries (consumable via `pkg-config`) comprising the eventual product.
You can link with the libraries selectively based on the features you need. Also, if MinGW64 finally provides a first-class implementation of a certain API family, you are
covered — simply replace the affected `-lsomething` flag.

Component|Maturity|Origin|Linkage|License|Description
---|---|---|---|---|---
[libwusers](https://github.com/treeswift/libwusers)|RC|in-house|`-lwusers`|public domain|`<pwd.h>` and `<grp.h>` (user and group API)
[libfatctl](https://github.com/treeswift/libfatctl)|RC|in-house|`-lfatctl`|public domain|*nix file API (e.g. the`*at` function family)
[libmemmap](https://github.com/treeswift/libmemmap)|β|in-house|`-lmemmap`|public domain|`<sys/mman.h>` virtual memory API
[libresolw](https://github.com/treeswift/libresolw)|baby steps|mixed|`-lresolw`|BSD|`<resolv.h>` API (domain name resolution, DNS)
[silverware](https://github.com/treeswift/silverware)|baby steps|in-house|`-lsilver`|public domain|*nix process API
[glob](https://github.com/treeswift/glob)|RC|3rdparty|`-lglob`|BSD|`glob()` and `fnmatch()` API
[getline](https://github.com/treeswift/getline-compatible)|β|3rdparty|`-lgetline`|ZLib|`getline` API (a very basic implementation)
[libob](https://github.com/treeswift/strptime)|RC|3rdparty|`-lstrptime` or `-lob`|MIT|the `strptime` function (highly configurable)

# Legal

Components we maintain ourselves are released into the [public domain](https://en.wikipedia.org/wiki/Public_domain) with a no-strings-attached [Unlicense License](LICENSE).

Components we have selected as useful third-party building bricks are released either [under a permissive license](https://en.wikipedia.org/wiki/Permissive_software_license) — such as BSD, Apache, MIT or CC-A — or right into the [public domain](https://en.wikipedia.org/wiki/Public_domain).

## Why?

While being entirely pro-free market, we don't believe in appropriation of ideas, and software is nothing but ideas.

We obey the copyright law because we don't think it's the right time for a publicly announced disobedience campaign, and for many other purely opportunisic reasons. However,
when it comes to the status of our own work, there is nothing at stake but our principles, and our principles are stated above: ideas are nothing but similarities, and there
is nothing in pure similarity that has anything in common with any form of property recognized by common law.

In certain theistic philosophies, ideas are created by God. In
the materialistic philosophy, there is simply no such thing; ideas are properties of matter (something that exists), and nothing more than _likenesses_ among something that
exists. One can own a red scarf, a red dress, a red hat, a red car or a red Japanese maple tree — etc., etc. All of them can be put under a lock or behind a fence, leased,
subleased, donated or trashed; but one can't own the red _color_. You can have three cars, three laptops, three homes, three passports of different countries — but you can't
own _the number three_, or any number, for that matter — and the digital representation of software is nothing but _numbers_.
In a nutshell, *there is no reasonable philosophy behind the copyright law — and can't be any.*

If you think that a conceptually unsound law is still worth enactment and enforcement on the grounds of the social benefits it brings, you might as well defend establishment
of a government-endorsed religion on those same grounds. We don't.

A legislated belief in the real existence of ideas, and in human _creation_ of ideas, is nothing better than a legislated belief in God.

### But, but, where'd I get my soup? (if you recognized a quote from _The Dog's Heart_, you got it right)

Read this: https://german.yale.edu/sites/default/files/hayek_-_the_use_of_knowledge_in_society.pdf

There is a common understanding among the theoreticians that one-off knowledge is powerless. Fewer people understand, however, that theoretical knowledge is zero-off.

The general principles powering nuclear weapons were talk of the town as early as in 1960es; these days, they are middle school curriculum. It's _hard_ to find a K12
student not knowing how A- and H-bombs work. However, the specific properties of the supercritical assembly that render the explosion guaranteed are still among the
most guarded government secrets. Uranium is sold on Amazon, but if you want to build your own Doomsday machine, you are out of luck. _Practical knowledge is infinitely
worthier than theoretical._

Behind every invenion and every software product — a _named_ achievement — there is a _sea_ of unnamed knowledge never shared with anyone because it is infinitely harder
to share. Read comments to the code of any open source project — do they make sense right away? If they do, someone will gladly read your CV.

The essence of the (c)/IP law is to present it to the public as if only _named_ knowledge mattered — and then, if you are lucky enough to to put a name on your knowledge,
demand the rent from those whose knowledge is unnamed.

In a sane world, you are paid for solving the problems other people face. It doesn't matter whether your knowledge is vetted or labeled by some established authority.
You don't need legislation or a court order to convince people that you are their only hope.

If you think you do — what reasonable person will be your friend?

# Extending LibMoreGW

If you'd like to 
* file a "missing feature" request;
* propose a component for inclusion into `libmoregw` —

GitHub provides the necessary tools. File an issue here: https://github.com/treeswift/libmoregw/issues

The three primary criteria for adoption of a certain component are
* the existence of actual POSIX/BSD/Linux/some*nix API it provides *used within a real software project you are developing or porting*;
* the _breadth_ of the component (i.e. whether it "does one thing and does it well");
* permissive license (see above).

