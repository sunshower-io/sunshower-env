# Sunshower environment

Welcome to Sunshower!  This is a place to start.

The environment POMs/BOMs define common functionality that's
used everywhere in the project.

## How releases are managed:

### Feature Branches
Most work should be done on a feature-branch, i.e. a vanilla Git branch (or fork).
These branches will be built and deployed automatically.  However, these builds may
be overwritten at any time by other feature-branch PRs, so it's best to use your
local Maven cache.

### Master/Main
The main branch is built automatially but *tagged* with the build-number.  
This allows dependents to refer to a specific build.

### Releasing

To release, navigate to your bill-of-materials file (typically `bom/pom.xml`) and make note
of the version (it should always be a SNAPSHOT locally).  From there:
1. Run `git checkout -b release/<VERSION>` where version is the version from your POM
1. Merge master via `git pull && git merge master`
1. Push to your branch--it will be built and released automatically

If everything goes well, 