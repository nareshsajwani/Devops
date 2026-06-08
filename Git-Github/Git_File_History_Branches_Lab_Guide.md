
GIT FILE HISTORY & BRANCHES - STEP BY STEP LAB NOTES
====================================================

PURPOSE
=======
This guide explains WHY files appear/disappear between branches,
HOW to view old file versions, and WHAT each command is doing.

------------------------------------------------------------------
LAB 1 - FILE EXISTS IN ONE BRANCH BUT NOT ANOTHER
------------------------------------------------------------------

STEP 1: Create Repository

    mkdir demo
    cd demo
    git init

What happened?
- Git created an empty repository.
- Current branch = master

--------------------------------------------------

STEP 2: Create First File

    echo "Version 1" > app.txt
    git add app.txt
    git commit -m "Initial version"

Repository:

    master
      |
      v
    Commit-A

Files:

    app.txt

--------------------------------------------------

STEP 3: Create Feature Branch

    git checkout -b feature

What happened?
- New branch created.
- Both branches point to same commit.

    master ----+
               |
               v
            Commit-A
               ^
               |
    feature ---+

--------------------------------------------------

STEP 4: Add New File In Feature Branch

    echo "Feature code" > feature.txt
    git add feature.txt
    git commit -m "Added feature file"

Repository:

          Commit-B (feature)
         /
    Commit-A (master)

Files visible in feature:

    app.txt
    feature.txt

--------------------------------------------------

STEP 5: Switch Back To Master

    git checkout master

Files visible:

    app.txt

Question:
Where did feature.txt go?

Answer:
feature.txt only exists in Commit-B.
master still points to Commit-A.

Git changed the working directory to match master.

--------------------------------------------------

STEP 6: Verify

    ls

Output:

    app.txt

Switch again:

    git checkout feature
    ls

Output:

    app.txt
    feature.txt

LESSON:
Branches can show different files because they point to different commits.

------------------------------------------------------------------
LAB 2 - VIEW HISTORY OF A FILE
------------------------------------------------------------------


STEP 1

    echo "Version 2" >> app.txt
    git add app.txt
    git commit -m "Updated app"

STEP 2

    echo "Version 3" >> app.txt
    git add app.txt
    git commit -m "Updated app again"

--------------------------------------------------

View History

    git log -- app.txt

Purpose:
Show all commits that modified app.txt

Example:

    Commit-3
    Commit-2
    Commit-1

------------------------------------------------------------------
LAB 3 - VIEW OLD VERSION OF A FILE
------------------------------------------------------------------

Find commit:

    git log --oneline

Example:

    ##abc111 Version 1
    ##abc222 Version 2
    ##abc333 Version 3
	
	7761eb8 (HEAD -> feature) Updated app again
	31d8920 Updated app
	f0e5603 Added feature file
	ed3de92 (master) Initial version	
	
--------------------------------------------------

View app.txt as it existed in Commit-1

    git show ed3de92:app.txt
	git show f0e5603:app.txt
	git show 31d8920:app.txt
	git show 7761eb8:app.txt
	


Result:

    Version 1

--------------------------------------------------

View app.txt as it existed in Commit-3

    git show 31d8920:app.txt

Result:

    Version 1
    Version 2

LESSON:
Git stores every committed version.


------------------------------------------------------------------
LAB 4 - COMPARE TWO FILE VERSIONS
------------------------------------------------------------------


Command:

    git diff ed3de92 31d8920 -- app.txt

Purpose:
Compare Version 1 and Version 3

Example Output:

    + Version 2
    + Version 3

Meaning:
These lines were added after Commit-1.


------------------------------------------------------------------
LAB 5 - SEE WHO CHANGED A LINE
------------------------------------------------------------------


Command:

    git blame app.txt

Example:

	^ed3de92 (Your Name 2026-06-03 16:44:52 +0000 1) Version 1
	31d89207 (Your Name 2026-06-03 16:50:50 +0000 2) Version 2
	7761eb88 (Your Name 2026-06-03 16:51:23 +0000 3) Version 3

Purpose:
Shows who last modified each line.

Useful during troubleshooting.

------------------------------------------------------------------
LAB 6 - RESTORE OLD VERSION OF FILE
------------------------------------------------------------------

Restore app.txt from Commit-1

	cat app.txt

    git checkout f0e5603 -- app.txt

Verify:

    cat app.txt

Result:

    Version 1

Commit if you want to keep restoration:

    git add app.txt
    git commit -m "Restored app.txt"


------------------------------------------------------------------
LAB 7 - UNDERSTANDING YOUR MERGE EXAMPLE
------------------------------------------------------------------


You executed:

    git checkout -b feature/tablespace-monitoring

Created:

    3462c2f

Then:

    git checkout master

Created:

    22f3435

Then:

    git checkout -b feature/ansible-automation

Created:

    83ce750

Then:

    git checkout master

Created:

    460bc2e

--------------------------------------------------

Before Merge

    master ----------------> 460bc2e

    feature/tablespace ----> 3462c2f

--------------------------------------------------

Merge Command

    git checkout master
    git merge feature/tablespace-monitoring

Git created:

    527c656

Verify:

    git show --pretty=raw 527c656

Output:

    parent 460bc2e
    parent 3462c2f

Meaning:

    527c656
    ├── parent #1 = 460bc2e
    └── parent #2 = 3462c2f

LESSON:
Merge commit has TWO parents.


------------------------------------------------------------------
MOST IMPORTANT COMMANDS
------------------------------------------------------------------


See current branch:

    git branch

See status:

    git status

See history:

    git log --oneline

See file history:

    git log -- app.txt

See old version:

    git show commit:file

Compare versions:

    git diff commit1 commit2 -- file

See who changed line:

    git blame file

Restore old file:

    git checkout commit -- file

See commit details:

    git show commit

See merge parents:

    git show --pretty=raw commit


------------------------------------------------------------------
MEMORY TRICKS
------------------------------------------------------------------


1. Branch = Pointer

2. Commit = Snapshot

3. HEAD = Current Position

4. Switching branch changes visible files

5. Git never loses committed history

6. Merge commit = Commit with 2 parents

7. File disappears because target branch does not contain it

8. Old file versions can always be viewed using:

       git show commit:file
