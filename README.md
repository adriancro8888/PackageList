[![Build Status](https://travis-ci.org/daveverwer/SwiftPMLibrary.svg?branch=master)](https://travis-ci.org/daveverwer/SwiftPMLibrary)

# The SwiftPM Library

This repository powers the list of packages indexed and monitored by the [SwiftPM Library](https://swiftpm.co). The intention of this repository is to build a *complete* list of packages that support the Swift Package Manager.

At some point, this list may be able to be replaced with an *official* list supplied by Apple and/or GitHub but until then, this is better than nothing.

## Adding packages

Please do submit your own, or other people's repositories to this list. There are a few requirements, but they are simple:

* Packages must have a Package.swift file (obviously?) in the root of the repository.
* Packages must be written in **Swift 4.0 or later**.
* Packages should declare at least one product in the Package.swift file. This can be either a library product, or an executable product. Packages can of course declare more than one product!
* Packages must have at least one release. A release is defined as a git tag that conforms to the [semantic version](https://semver.org) spec. This can be a [beta or a pre-release](https://semver.org/#spec-item-9) semantic version, it does not necessarily need to be stable.
* Packages should compile without errors. Actually, this isn't a strict requirement but it's probably a good idea since you're about to add it to a package directory.
* Packages should output valid JSON when `swift package dump-package` is run with the latest version of the Swift tools. Please check that you can execute this command in the root of the package directory before submitting.
* The full HTTPS clone URL for the repository should be submitted, including the .git extension.
* Packages can be on *any* publicly available git repository, not just GitHub. Just add the full HTTPS clone URL.

**Note:** There's no gatekeeping or quality threshold to be included in this list. The [library itself](https://swiftpm.co) sorts package search results by a number of metrics to place mature, good quality packages higher in the results.

## How do you add a package?

It's simple. Just fork this repository, edit the JSON, and submit a pull request. If you plan to submit a set of packages, there is no need to submit each package in a separate pull request. Feel free to bundle multiple updates at once as long as all packages match the criteria above.

## JSON validation

[Travis has been configured](https://travis-ci.org/daveverwer/SwiftPMLibrary) to validate JSON for every pull request. If you would like to run this validation locally before submitting, the commands to verify and sort JSON are listed below. These commands use [jq](https://stedolan.github.io/jq/) to do this.

To validate:

```shell
jq -e . packages.json > /dev/null
```

Then, to sort:

```shell
echo "$(jq 'sort_by(ascii_downcase)' packages.json)" > packages.json
```

Make sure there are no dupes (no dupe variants w/ .git and w/o, no case differences):
```shell
(for repo in $(jq '.[]' packages.json); do basename $repo; done) \
  | tr '[:upper:]' '[:lower:]' \
  | sed 's|"||g' | sed s/.git//g \
  | uniq -d
```
