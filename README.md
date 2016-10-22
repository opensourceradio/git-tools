# git-tools
Git tools used when working with the opensourceradio repos.

As of now, this repo contains only my versions of tools snagged from other places on the interwebs. See, e.g., http://stackoverflow.com/questions/384108/moving-from-cvs-to-git-id-equivalent and http://stackoverflow.com/questions/16524225/how-can-i-populate-the-git-commit-id-into-a-file-when-i-commit for references.

## Three Things Required

1. A pair of scripts to manipulate the source files

* `add-hash` is a ruby script that's used to grab the current commit hash on checkout and insert it into any file that includes the string `$Hash$`
* `clean-hash` is a perl script that removes all commit hashes from strings in any file on commit.

  These scripts should be in your `${PATH}`.

2. Your git configuration (system, user, or local) must include the following in order to use these scripts:

```
git config --add filter.buildsub.clean clean-hash
git config --add filter.buildsub.smudge add-hash
```

3. Your local repo must include a _.gitattributes_ file containing:
```
* filter=buildsub
```

Note that the filter name is arbitrary: the filter name in the two configuration settings, and the filter setting in _.gitattributes_ must match.
