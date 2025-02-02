# OpenIM Branch Management and Versioning: A Blueprint for High-Grade Software Development

[📚 **OpenIM TOC**](#openim-branch-management-and-versioning-a-blueprint-for-high-grade-software-development)
  - [Unfolding the Mechanism of OpenIM Version Maintenance](#unfolding-the-mechanism-of-openim-version-maintenance)
  - [Main Branch: The Heart of OpenIM Development](#main-branch-the-heart-of-openim-development)
  - [Release Branch: The Beacon of Stability](#release-branch-the-beacon-of-stability)
  - [Tag Management: The Cornerstone of Version Control](#tag-management-the-cornerstone-of-version-control)
  - [Release Management: A Guided Tour](#release-management-a-guided-tour)
  - [Milestones, Branching, and Addressing Major Bugs](#milestones-branching-and-addressing-major-bugs)
  - [Version Skew Policy](#version-skew-policy)
  - [Applying Principles: A Git Workflow Example](#applying-principles-a-git-workflow-example)
  - [Docker Images Version Management](#docker-images-version-management)


At OpenIM, we acknowledge the profound impact of implementing a robust and efficient version management system, hence we abide by the established standards of [Semantic Versioning 2.0.0](https://semver.org/lang/zh-CN/).

Our software blueprint orchestrates a tripartite version management system that integrates the `main` branch, the `release` branch, and `tag` management. These constituents operate in synchrony to preserve the reliability and traceability of our software across various stages of development.

## Unfolding the Mechanism of OpenIM Version Maintenance

Our version maintenance protocol revolves around two primary branches, namely: `main` and `release`. We resort to Semantic Versioning 2.0.0 for marking distinctive versions of our software, representing substantial milestones in its evolution.

In the OpenIM repository, version identification strictly complies with the `MAJOR.MINOR.PATCH` protocol. Herein:

- The `MAJOR` version indicates a shift arising from incompatible changes to the API.
- The `MINOR` version suggests the addition of features in a backward-compatible manner.
- The `PATCH` version flags backward-compatible bug fixes.

## Main Branch: The Heart of OpenIM Development

The `main` branch is the operational heart of our development process. Housing the most recent and advanced features, this branch serves as the nerve center for all enhancements and updates. It encapsulates the freshest, though possibly unstable, facets of the software. Visit our `main` branch [here](https://github.com/openimsdk/open-im-server/tree/main).

## Release Branch: The Beacon of Stability

For every major release, we curate a corresponding `release` branch, e.g., `release-v3.1`. This branch symbolizes an embodiment of stability and ensures an updated version of the software, providing a dependable option for users favoring stability over nascent, yet possibly unstable, features. Visit the `release-v3.1` branch [here](https://github.com/openimsdk/open-im-server/tree/release-v3.1).

## Tag Management: The Cornerstone of Version Control

In OpenIM's version control system, the role of `tags` stands paramount. Owing to their immutable nature, tags can be effectively utilized to retrieve a specific version of the software. Explore our library of tags [here](https://github.com/openimsdk/open-im-server/tags).

Our Docker image versions are intimately entwined with these tripartite components. For instance, a Docker image tag may correspond to `ghcr.io/openimsdk/openim-server:v3.1.0`, a release to `ghcr.io/openimsdk/openim-server:release-v3.0`, and the main branch to `ghcr.io/openimsdk/openim-server:main` or `ghcr.io/openimsdk/openim-server:latest`.

To further clarify, the semantics of our version numbers are as follows:

- **Revision version number**: This represents bug fixes or code optimizations. Typically, it entails no new feature additions and ensures backward compatibility.
- **Build version number**: Auto-generated by the system, each code submission prompts an automatic increment by 1.
- **Version modifiers**: These hint at the software's development stage and stability. Some commonly used modifiers are `alpha`, `beta`, `rc`, `ga`, `r/release/or nothing`, and `lts`.
  - `alpha`: An internal testing version with numerous bugs, typically used for communication among developers.
  - `beta`: A test version with numerous bugs, generally used for testing by eager community members, who provide feedback to the developers.
  - `rc`: Release candidate, which is to be released as the official version. It's the last test version before the official version.
  - `ga`: General Availability, the first stable release.
  - `r/release/or nothing`: The final release version, intended for general users.
  - `lts`: Long Term Support, the official will specify the maintenance year for this version and will fix all bugs discovered in this version.

Whenever a project undergoes a partial functional addition, the minor version number increments by 1, resetting the revision version number to 0. In contrast, any major project overhaul results in an increment by 1 in the major version number. The build number, typically auto-generated during the compilation process, only requires format definition, thereby eliminating manual control.

## Release Management: A Guided Tour

Our GitHub repository at https://github.com/openimsdk/open-im-server/releases associates a release with each tag, with a distinction between Pre-release and Latest, determined by the branch source. Every significant feature launch prompts the issue of a `release` branch, such as `release-v3.2`, as a beacon of stability and Latest release.

Pre-releases correspond to releases from the `main` branch, denoting tags with Version modifiers such as `v3.2.1-beta.0`, `v3.2.1-rc.1`, etc. If you are seeking the most recent, albeit possibly unstable, release with new features, these tags, originating from the latest `main` branch code, are your go-to.

Conversely, if stability is your primary concern, you should opt for the release tagged Latest, denoted by tags without Version modifiers, such as `v3.2.1`, `v3.2.2` etc. These tags are linked to the latest stable maintenance branch, like `release-v3.2`.

## Milestones, Branching, and Addressing Major Bugs

**About:**

+ [OpenIM Milestones](https://github.com/openimsdk/open-im-server/milestones)
+ [OpenIM Tags](https://github.com/openimsdk/open-im-server/tags)
+ [OpenIM Branches](https://github.com/openimsdk/open-im-server/branches)

We create a new branch, such as `release-v3.1`, for each significant milestone (e.g., v3.1.0), housing all relevant code for that release. All enhancements and bug fixes targeting the subsequent version (e.g., v3.2.0) are integrated into this branch.

`PATCH` versions (represented by Z in `X.Y.Z`) are primarily propelled by bug fixes, and their release may be either priority-driven or scheduled. In contrast, `MINOR` versions (represented by Y in `X.Y.Z`) are contingent upon the project's roadmap, milestone completion, or a pre-established timeline, always maintaining backward-compatible APIs.

When dealing with major bugs, we selectively merge the fix into the affected version (e.g., v3.1 or the `release-v3.1` branch), as well as the `main` branch. This dual pronged strategy ensures that users on older versions receive crucial bug fixes, while also keeping the `main` branch updated.

We reinforce our approach to branch management and versioning with stringent testing protocols. Automated tests and code review sessions form vital components of maintaining a robust and reliable codebase.

## Version Skew Policy

This document describes the maximum version skew supported between various openim components. Specific cluster deployment tools may place additional restrictions on version skew.


### Supported version skew

In highly-available (HA) clusters, the newest and oldest `openim-api` instances must be within one minor version.

### OpenIM Versioning, Branching, and Tag Strategy

Similar to Kubernetes, OpenIM has a strict versioning, branching, and tag strategy to ensure compatibility among its various services and components. This document outlines the policies, especially focusing on the version skew supported between OpenIM's components. Given that the current version is v3.3, the policy references will be centered around this version.

#### Supported Version Skew

##### openim-api

In highly-available (HA) clusters, the newest and oldest `openim-api` instances must be within one minor version.

Example:

+ Newest `openim-api` is at v3.3
+ Other `openim-api` instances are supported at v3.3 and v3.2

##### openim-rpc-* Components

All `openim-rpc-*` components (e.g., `openim-rpc-auth`, `openim-rpc-conversation`, etc.) should adhere to the following rules:

1. They must not be newer than `openim-api`.
2. They may be up to one minor version older than `openim-api`.

Example:

+ `openim-api` is at v3.3
+ All `openim-rpc-*` components are supported at v3.3 and v3.2

Note: If version skew exists between `openim-api` instances in an HA cluster, this narrows the allowed `openim-rpc-*` components versions.

##### Other OpenIM Services

Other OpenIM services such as `openim-cmdutils`, `openim-crontask`, `openim-msggateway`, etc. should adhere to the following rules:

1. These services must not be newer than `openim-api`.
2. They are expected to match the `openim-api` minor version but may be up to one minor version older (to allow live upgrades).

Example:

+ `openim-api` is at v3.3
+ `openim-msggateway`, `openim-cmdutils`, and other services are supported at v3.3 and v3.2

#### Supported Component Upgrade Order

The version skew policy has implications on the order in which components should be upgraded. Below is the recommended order to transition an existing cluster from version v3.2 to v3.3:

##### openim-api

Pre-requisites:

1. In a single-instance cluster, the existing `openim-api` instance is v3.2.
2. In an HA cluster, all `openim-api` instances are at v3.2 or v3.3.
3. All `openim-rpc-*` and other OpenIM services communicating with this server are at version v3.2.

Upgrade Procedure:

1. Upgrade `openim-api` to v3.3.

##### openim-rpc-* Components

Pre-requisites:

1. The `openim-api` instances these components communicate with are at v3.3.

Upgrade Procedure:

2. Upgrade all `openim-rpc-*` components to v3.3.

##### Other OpenIM Services

Pre-requisites:

1. The `openim-api` instances these services communicate with are at v3.3.

Upgrade Procedure:

2. Upgrade other OpenIM services such as `openim-msggateway`, `openim-cmdutils`, etc., to v3.3.

#### Conclusion

Just like Kubernetes, it's essential for OpenIM to have a strict versioning and upgrade policy to ensure seamless operation and compatibility among its various services. Adhering to the policies outlined above will help in achieving this goal.


## Applying Principles: A Git Workflow Example

The workflow to address a bug fix might follow these steps:

```bash
# Checkout the branch for the version that needs the bug fix
git checkout release-v3.1

# Create a new branch for the bug fix
git checkout -b bug/bug-name

# ... Make changes, commit your work ...

# Push the branch to your remote repository
git push origin bug/bug-name

# After the pull request is merged into the release-v3.1 branch, 
# checkout and update your main branch
git checkout main
git pull origin main

# Merge or rebase the changes from release-v3.1 into main
git merge release-v3.1

# Push the updates to the main branch
git push origin main
```
##  Release Process

```
Publishing v3.2.0: A Step-by-Step Guide
(1) Create the tag v3.2.0-alpha.0 from the main branch.
(2) Bugs are fixed on the main branch. Once the bugs are resolved, tag the main branch as v3.2.0-rc.0.
(3) After further testing, if v3.2.0-rc.0 is deemed stable, create a branch named release-v3.2 from the tag v3.2.0-rc.0.
(4) From the release-v3.2 branch, create the tag v3.2.0. At this point, the official release of v3.2.0 is complete.

After the release of v3.2.0, if urgent bugs are discovered, fix them on the release-v3.2 branch. Then, submit two pull requests (PRs) to both the main and release-v3.2 branches. Tag the release-v3.2 branch as v3.2.1.
```

Throughout this process, active communication within the team is pivotal to maintaining transparency and consensus on changes.

## Docker Images Version Management

For more details on managing Docker image versions, visit [OpenIM Docker Images Administration](https://github.com/openimsdk/open-im-server/blob/main/docs/conversions/images.md).
