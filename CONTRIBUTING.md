## Pull request model

Writing the manuscript in this repository uses a development model with the following features:

* There are two main branches: `draft-branch` and `master`. 
`draft-branch` is akin to a development branch and `master` contains a more complete or "production-ready" draft of the manuscript.
* Contributors are expected to create feature branches and file pull requests against `draft-branch`.
* Pull requests must be reviewed and approved before merging to `draft-branch`. 
These should be limited in scope (see below).
Review at this stage serves to provide constructive feedback, catch issues like typos or problems formatting citations, and, more generally, to raise co-authors awareness of others' work in service of a cohesive manuscript.
* Pull requests from `draft-branch` to `master` should consist of entire sections of the manuscript.
These also must be reviewed and approved before merging.
Review at this stage allows us to discuss the larger contours and messaging of the paper.

### Branch naming

To avoid confusion or conflicts, we use the following feature branch naming convention:

```
<GitHub user name>/<purpose of the branch>
```

It may also be helpful to include the issue number in your branch name.
For example, the branch @jaclyn-taroni used to add contributing guidelines and address [#18](https://github.com/jaybee84/ml-in-rd/issues/18) was:

```
jaclyn-taroni/18-contributing
```

### Pull request composition and scope

Pull requests to `draft-branch` should be small and focused enough in scope such that your reviewer can provide detailed feedback. (Think 2-3 paragraphs as a rule of thumb!) 

Pull requests from `draft-branch` to `master` should consist of entire sections of the manuscript.

### Spellcheck as part of pull requests

We have [spellcheck](USAGE.md#spellchecking) enabled as part of an AppVeyor workflow.
The dictionary used for spellchecking can be updated.
Edit the file in `build/assets/custom-dictionary.txt` by adding new entries to the end.
You do not need to change anything else.
However, if you want to update the first line to have an accurate count of words and you want to remove non-unique ones, run the following command from within `build/assets` on your favorite OS X or Linux machine:

```
(( len = $(awk '!a[$0]++' < custom-dictionary.txt | wc -l ) - 1 )); tmpfile="$(mktemp)"; echo "personal_ws-1.1 en $len utf-8" > $tmpfile; tail -n +2 custom-dictionary.txt | awk '!a[$0]++' >> $tmpfile; mv $tmpfile custom-dictionary.txt
```

_[Adapted from OpenPBTA manuscript](https://github.com/AlexsLemonade/OpenPBTA-manuscript/blob/master/.github/PULL_REQUEST_TEMPLATE.md#spellcheck-step)_
