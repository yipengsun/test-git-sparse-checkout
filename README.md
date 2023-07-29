# test-git-spare-checkout

First do the following

1. Clone this repo with `git clone --filter=blob:none --no-checkout`
2. `git sparse-checkout add --sparse README.md`
3. `git sparse-checkout reapply`
4. `git checkout`

Now there should be just a single `README.md` in project root.

Now, say you want to add a new file `stuff.txt` in `folder1`:

1. `mkdir folder1`
2. `touch folder1/stuff.txt`
3. A naive `git add folder1/stuff.txt` would produce the following error:

    ```
    The following paths and/or pathspecs matched paths that exist
    outside of your sparse-checkout definition, so will not be
    updated in the index:
    folder1/blank
    hint: If you intend to update such entries, try one of the following:
    hint: * Use the --sparse option.
    hint: * Disable or modify the sparsity rules.
    hint: Disable this message with "git config advice.updateSparsePath false"
    ```

4. To actually add the file, follow the first hint provided by git:

    ```
    git add --sparse folder1/stuff.txt
    ```


Above is tested with `git version 2.38.4`.
