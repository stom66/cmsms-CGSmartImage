# CGSmartImage (maintained fork)

Calguy's Smart Image Toolkit: the `{CGSmartImage}` tag and related plugins that resize, crop, filter, watermark and cache images (GD), with responsive/device-aware output.

This repository is a **community-maintained fork** of the CGSmartImage module for
[CMS Made Simple](https://www.cmsmadesimple.org) (CMSMS), originally written by
Robert Campbell (*calguy1000*).

## Why this fork exists

The original author left the CMSMS project and the CG ("Calguy") modules will
not receive any further official releases. Many sites still depend on them, and
the last releases predate PHP 8: on current PHP they log large numbers of
deprecations, and some features stop with fatal errors.

Rather than patching the copy inside every site separately, the fixes live
here, in one place, so every site can use the same tested code and new fixes
only have to be made once.

## Compatibility

| | |
|---|---|
| Based on | CGSmartImage **1.22.7** (final upstream release) |
| Tested with | CMS Made Simple 2.2.24, Smarty 4.5.5, **PHP 8.5.12**, AlmaLinux 9 / Apache 2.4 |
| Minimum CMSMS | 2.2.9 (unchanged from upstream) |
| Requires | **CGExtensions** ≥ 1.61 (declared), and the PHP GD extension. |

## Version number

The module still reports version **1.22.7**, deliberately. If the version
in `moduleinfo.ini` / `GetVersion()` is raised, CMSMS treats the module as
needing an upgrade and **will not load it** until someone runs the upgrade in
Module Manager. Keeping the upstream version means the fork can be dropped
into an existing site with no database step. Fork changes are tracked by this
repository's commits (and tags, when made) instead.

## Installing / updating a site

The folder name must be exactly `CGSmartImage`.

```sh
# new install of the fork into a site
cd /path/to/site/modules
mv CGSmartImage CGSmartImage.orig          # keep the old copy until verified, then delete it
git clone <this-repository-url> CGSmartImage

# later updates
cd /path/to/site/modules/CGSmartImage && git pull
```

After replacing or updating the files, clear the CMSMS cache
(Admin → Site Admin → System Maintenance → Clear Cache). Make sure the web
server does not serve the `.git` folder (e.g. block dot-directories in
`.htaccess`).

## Changes in this fork

The first commit is the unmodified upstream release; every later commit is one
fix:

- fix(CGSmartImage): mark CGImageBase ArrayAccess methods #[\ReturnTypeWillChange]

See each commit message for the error it fixes and how it was verified.

## Known issues

- None known. Note that `filter_watermark` relies on CGExtensions; use this fork's CGExtensions (the upstream one crashes on PHP 8 when a watermark follows another filter).

## Contributing

- One fix per commit, using [Conventional Commits](https://www.conventionalcommits.org)
  (`fix:`, `feat:`, `perf:` …), with the error message and how you tested it.
- Keep behaviour and rendered output unchanged unless the change is the fix.
- Test against the PHP versions in the table above (`php -l` is not enough:
  load the classes and exercise the feature, since many PHP 8 problems only
  appear at runtime).
- Don't change the version number (see above).

## Licence

GNU General Public License, version 2 or (at your option) any later version,
with the upstream author's additional condition, repeated from the source file
headers:

> However, as a special exception to the GPL, this software is distributed as
> an addon module to CMS Made Simple. You may not use this software in any Non
> GPL version of CMS Made simple, or in any version of CMS Made simple that does
> not indicate clearly and obviously in its admin section that the site was
> built with CMS Made simple.

Copyright © Robert Campbell (calguy1000) and contributors. The full GPL text is
in [`COPYING`](COPYING).
