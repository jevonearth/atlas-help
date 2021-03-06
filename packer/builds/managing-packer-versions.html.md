---
title: "Managing Packer Versions"
---

# Managing Packer Versions

Atlas does not automatically upgrade the version of Packer
used to run builds or compiles. This is intentional, as occasionally
there can be backwards incompatible changes made to Packer that cause templates to stop
building properly, or new versions that produce some other unexpected behavior.

All upgrades must be performed by a user, but Atlas will display a notice
above any builds run with out of date versions. We encourage the use
of the latest version when possible.

### Upgrading Packer

1. Go the Settings tab of a build configuration or application
1. Go to the "Packer Version" section and select the version you
wish to use
1. Review the changelog for that version and previous versions
1. Click the save button. At this point, future builds will use that
version
