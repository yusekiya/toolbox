# Toolbox

My toolbox for better terminal life.

## `note`

Minimal note-taking script.
Only two commands, `note add` and `note search`, are supported.

### Requirements for default configuration

- `python3` to run this script.
- [`toml`][toml] python package to load a configuration file.
- [`ag`][ag], which makes a list of lines.
  Each line consists of a file path of a note and keywords for the note.
- [`fzf`][fzf], which filters the list by keywords.
- `sed`, which formats each line for good looking when you filter the list with the keywords.
- `perl`, which extracts a relative file path from the root of the note directory.

[toml]: https://github.com/uiri/toml
[ag]: https://github.com/ggreer/the_silver_searcher
[fzf]: https://github.com/junegunn/fzf

### Example

- Make a new markdown file

    ```shell
    $ note add
    Enter comma-separated list of keywords: <keyword1>, <keyword2>, ...
    ```

    This command opens an editor specified by the environment variable `EDITOR` to edit the markdown file.

- View a note

    ```shell
    $ less `note search`
    or
    $ less `note search <keyword1> <keyword2> ...`
    ```

    The `note search` command narrows your search results using a fuzzy search command,
    and returns the path to the selected note file.
    You can open the file with viewer commands such as `less`, `more`, and others.

- Edit a note

    ```shell
    $ vim `note search`
    or
    $ vim `note search <keyword1> <keyword2> ...`
    ```

    You can use your favorite editor to edit the file.

### Configuration

The configuration file `config.toml` with default options is created in the `~/.note` directory
when you run the command for the first time.
Here is the list of variables.

| variable               | description                                                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `note_dir`             | Root directory under which notes are saved.                                                                               |
| `dir_format`           | Name format of subdirectories in the `note_dir`. This is useful for storing notes in date-based directories. [Standard date time format][date_format] can be used.                   |
| `file_name_format`     | Note file name format. The file must have `.md` filename extension. You can use [standard date time format][date_format]. |
| `file_search_command`  | Command and options to make the list of notes.                                                                            |
| `format_line_command`  | Command and options to format the list.                                                                                   |
| `filter_command`       | Command and options to filter the list.                                                                                   |
| `get_filename_command` | Command and options to extract the relative path.                                                                         |

The `note add` creates a new markdown file whose full path is formatted as `note_dir/dir_format/file_name_format`.

The `note search` searches for notes and returns a relative file path using the following pipeline process.

```shell
$ file_search_command | format_line_command | filter_command | get_filename_command
```

You can modify the `*-command` variables so that the above pipeline works in you environment.


[date_format]: https://docs.python.org/3/library/time.html#time.strftime


## `git-deploy`

Copy git tracking files to another directory.

### Requirements

- git
- rsync

### Example

- Copy files to a remote directory

    ```shell
    $ git deploy <user>@<host>:<directory>
    ```

- Copy files to a local directory

    ```shell
    $ git deploy -l <directory>
    ```

## `git-manage`

Utilities to keep managed git repositories up to date.

### Requirements

- [git-repo-updater]

[git-repo-updater]: https://github.com/earwig/git-repo-updater


## `start_new_study` and `add_project`

Script to create template directory for study.

## `today` and `todaymd`

Print date of today. It is useful for making directories and files.

## `show_colors`

Print a list of color codes in its color.

## `trimtemp`

Remove `temp` prefix from a file name.