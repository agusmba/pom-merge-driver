pom-merge-driver
================

Custom Git merge driver for Maven's pom.xml.

If there was a change in the project version in a
branch to be merged (while this change was not merged
yet), use their version to avoid conflicts and be
consistent in case of trivial merges that might happen
at the same time. All other changes in the file will
be merged as usual.

Before committing however, the project version is reverted
back to its previous value, unless on master branch.
This allows for gitflow release-finish, hotfix-finish,
and feature-finish to work better.

If Git configuration variable "merge.pommerge.keepmasterversion"
is set to true, the project version is always reverted
even on master branch.

Installation
-------------

git-config:
<pre>
[merge "pommerge"]
        name = A custom merge driver for Maven's pom.xml
        driver = $PATH_TO/mergepom.py %O %A %B
</pre>
"$PATH_TO" needs to be replaced with the full path to "mergepom.py".

.gitattributes
<pre>
pom.xml merge=pommerge
</pre>
