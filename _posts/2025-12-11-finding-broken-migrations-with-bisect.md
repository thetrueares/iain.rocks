---
layout: post
title: "Finding broken migrations with Bisect"
date: "2025-08-19 06:18:40 +0200"
categories: [AI]
author: Iain Cambridge
---
I just watched [Pauline Vos'](https://gitlegit.dev/) ["The Business of Bisecting"](https://www.youtube.com/watch?v=uzog0BTLrYY) talk, and one of the questions from the audience really stuck with me. During the section on automating good/bad commit checks with a script, someone asked if git passes the commit hash of the previous commit to the script, which it doesn't. But the question was the wrong one. The real question should be "Can you get the hash of the previous commit?" Which you can. And it's super useful if you want to check if a migration or something similar is broken.

# What is bisect

The best way to learn is to watch ["The Business of Bisecting"](https://www.youtube.com/watch?v=uzog0BTLrYY), since that's literally what I watched to learn. But here's the quick version for those just wanting to read.

Bisect helps you trace through commits to find where something changed. It's incredibly powerful and can save you hours of manually searching through code. Say you want to find when a test started breaking locally while still passing in CI—a frustrating scenario where the culprit isn't immediately obvious.

You start by marking a commit as "good" where you know everything worked. This becomes your baseline. Then you check each commit to see if it works or not. Git uses binary search to efficiently narrow down the problem, so you won't check every single commit. Mark each one good or bad, and git intelligently picks the next commit to check, cutting the search space in half each time. You can automate this entire process with a script, saving yourself hours of tedious work. A bash script handles all the repetitive tasks automatically. Once you've set it up, the script runs through each step without any intervention, freeing you up to focus on more important things.

Eventually, git bisect pinpoints the exact commit that introduced the bug. You can examine those specific changes and fix the issue much faster than hunting it down manually.

# Scenario

You might need to retrieve an earlier revision when debugging issues or verifying backward compatibility. In this example, we'll restore a database schema from a previous point in time, then run migrations against it. This helps us find migrations that break due to schema changes—like when a migration expects a column that no longer exists, or tries to create something that's already there. Migrations can also break because of the data itself—unexpected NULL values, invalid foreign keys, or data that doesn't conform to new constraints. You could solve this by restoring a full database snapshot with representative data and migrating it forward, but for our purposes, testing schema changes alone catches the most common migration failures without the overhead of maintaining complete database dumps.

Luckily, git is predictable and makes this manageable. Bisect just moves where you are in the branch you're on during bisect so HEAD is the current place in the branch, just like during normal git operations. Any command you'd normally use with HEAD works here without special modifications. We can fetch commit IDs using `git rev-parse HEAD` and `git rev-parse HEAD~1`. Store them in variables, use `git checkout` to navigate back to the previous revision, then run whatever commands you need. Once everything's working, checkout the current revision again and complete your bisect operation. This straightforward approach gives you full control while leveraging git's reliable version control.

In my example, I'm using doctrine migrations within a Symfony app but change to your setup.

```bash
#!/bin/bash

## Get commit hashes
CURRENT_COMMIT=$(git rev-parse HEAD)
LAST_COMMIT=$(git rev-parse HEAD~1)

## Setup previous commit
git checkout "$LAST_COMMIT"
composer install --no-interaction > /dev/null 2>&1
./bin/console doctrine:database:drop --force --no-interaction > /dev/null 2>&1
./bin/console doctrine:database:create --if-not-exists --no-interaction > /dev/null 2>&1
./bin/console doctrine:schema:drop --force > /dev/null 2>&1
./bin/console doctrine:schema:create > /dev/null 2>&1
./bin/console doctrine:migrations:version --add --all --no-interaction > /dev/null 2>&1

## Setup current commit
git checkout "$CURRENT_COMMIT"
composer install --no-interaction > /dev/null 2>&1

# Actual test
./bin/console doctrine:migrations:migrate --no-interaction --allow-no-migration

MIGRATION_EXIT_CODE=$?
if [ $MIGRATION_EXIT_CODE -eq 0 ]; then
    # Migration succeeded: This is a "Good" commit
    exit 0
else
    # Migration failed: This is a "Bad" commit
    exit 1
fi
```

# Example

Blog posts are cool, but many of us learn by doing. I created a branch on my BillaBear project from a stable tag and added a breaking migration. Checkout the repository and run the following commands to see it work:

```sh
git clone https://github.com/billabear/billabear.git
cd billabear
git checkout bisect-migrations-example
git bisect start HEAD  # Marks the current commit (HEAD) as the starting point.
git bisect bad         # Explicitly marks the starting point as "bad".
git bisect good HEAD~20 # Marks the commit 20 commits prior to HEAD as "good".
git bisect run ./bisect-script.sh
```

You can then move the broken migration commit which is `03e7e4537f3c7be3540fd637b1fe48eca1b156f9` around using rebase and play around.