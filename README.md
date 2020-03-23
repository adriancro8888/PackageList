[![Build Status](https://travis-ci.org/daveverwer/SwiftPMLibrary.svg?branch=master)](https://travis-ci.org/daveverwer/SwiftPMLibrary)

# The SwiftPM Library

This repository powers the list of packages indexed and monitored by the [SwiftPM Library](https://swiftpm.co). The intention of this repository is to build a *complete* list of packages that support the Swift Package Manager.

At some point, this list may be able to be replaced with an *official* list supplied by Apple and/or GitHub but until then, this is better than nothing.

## Adding packages

Please feel free to submit your own, or other people's repositories to this list. There are a few requirements, but they are simple:

* Packages must have a Package.swift file (obviously?) located in the root of the repository.
* Packages must be written in **Swift 4.0 or later**.
* Packages must declare at least one product in the Package.swift file. This can be either a library product, or an executable product. Packages can of course declare more than one product!
* Packages should have at least one release. A release is defined as a git tag that conforms to the [semantic version](https://semver.org) spec. This can be a [beta or a pre-release](https://semver.org/#spec-item-9) semantic version, it does not necessarily need to be stable.
* Packages should compile without errors. Actually, this isn't a strict requirement but it's probably a good idea since you're about to add the package to a package directory.
* Packages must output valid JSON when `swift package dump-package` is run with the latest version of the Swift tools. Please check that you can execute this command in the root of the package directory before submitting.
* The full HTTPS clone URL for the repository should be submitted, including the .git extension.
* The repository must be publicly accessible.
* Packages can be on *any* repository host, not just GitHub. Just add the full HTTPS clone URL.

**Note:** There's no gatekeeping or quality threshold to be included in this list. The [library itself](https://swiftpm.co) sorts package search results by a number of metrics to place mature, good quality packages higher in the results.

## How do you add a package?

It's simple. Fork this repository, edit the JSON, and submit a pull request. If you plan to submit a set of packages, there is no need to submit each package in a separate pull request. Feel free to bundle multiple updates at once as long as all packages match the criteria above.

## JSON validation

[Travis is configured](https://travis-ci.org/daveverwer/SwiftPMLibrary) to validate JSON for every pull request. Please run this validation locally before submitting by running the [included validation script](./validate.swift), like so:


```shell
swift ./validate.swift diff
```
