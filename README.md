# Chef Run Recorder Cookbook

[![License](https://img.shields.io/github/license/ualaska-it/checksum_file.svg)](https://github.com/ualaska-it/checksum_file)
[![GitHub Tag](https://img.shields.io/github/tag/ualaska-it/checksum_file.svg)](https://github.com/ualaska-it/checksum_file)

__Maintainer: OIT Systems Engineering__ (<ua-oit-se@alaska.edu>)

## Purpose

This simple cookbook provides one resource that calculates a checksum, then writes it to a file.
The resource will signal convergence only if the content of the file changes.

The most common use of the checksum_file resource is to implement idempotence in a more robust fashion than looking at a single file.
One caveat is that this resource takes longer than checking for the creation of a single file, so may be prohibitive for very large directories.
However, the resource performs at most a tar and an md5sum on the target, and has been used for source trees of popular open-source projects without significant overhead compared to an entire Chef run.

## Requirements

### Chef

This cookbook requires Chef 14+

### Platforms

Supported Platform Families:

* Debian
  * Ubuntu, Mint
* Red Hat Enterprise Linux
  * Amazon, CentOS, Oracle
* Suse
* Windows

Platforms validated via Test Kitchen:

* Ubuntu
* Debian
* CentOS
* Oracle
* Fedora
* Amazon
* Suse
* Windows

Notes:

* This cookbook should support any recent Windows or Linux variant.

### Dependencies

This cookbook does not constrain its dependencies because it is intended as a utility library.
It should ultimately be used within a wrapper cookbook.

## Resources

This cookbook provides one resource for saving checksum.

### checksum_file

This resource provides a single action to save a checksum to a file.

__Actions__

One action is provided.

* `:save` - Post condition is that the checksum and path of the source file is written to the target file.

__Attributes__

This resource has five attributes.

* `source_path` - Required.
The local path to the file (regular file or directory) for which the checksum is to be calculated.
* `target_path` - Defaults to the name of the resource if not set explicitly.
The local path to which to write the path and checksum.
* `save_path` - Defaults to `true`.
Determines if the path information is saved along with the checksum.
If true, a change to the target path will cause the resource to converge and signal subscribers.
The source path is canonicalized before saving so relative, absolute, double dots, and multiple slashes do not matter.
* `checksum_algorithm` - Default to `md5`.
The algorithm to use.
Supported values are `md5` and `sha1`, not case sensitive.
* `include_metadata` - Default to `true`.
Determines if file metadata (permissions, times) are included in the checksum.
If false, only file content will affect checksum.
It is typically faster to include metadata.

## Recipes

This cookbook provides no recipes.

## Examples

Custom resources can be used as below.

```ruby
```

## Development

See CONTRIBUTING.md and TESTING.md.
