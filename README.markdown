Gistpaste: Command line paste script
====================================

This script can do all that the [defunkt gist script](http://github.com/defunkt/gist/tree) can:

- paste a file
- paste from stdin
- authenticate

Plus a few things it can't:

- paste multiple files at once
- paste clipboard output
- post anonymously even if a global git config exists
- specify file name
- specify file type

This script cannot "read" gists like defunkt's script can.  I
plan to create a gistcopy script for that at some point.

Installation
------------

Download and install

    wget http://github.com/dblevins/gistpaste/raw/master/gistpaste &&
    chmod 755 gistpaste &&
    sudo mv gistpaste /usr/local/bin/

Add any Perl modules you may not have

    sudo cpan LWP::UserAgent

And an optional module if your system's "which" command is disabled
for security reasons

    sudo cpan File::Which

Usage
-----

__gistpaste__ [options] [FILE...]

Paste file(s)

    gistpaste thatfile.txt another.diff

Paste STDIN

    grep "this" thatfile.txt | gistpaste
 

Paste the clipboard contents

    gistpaste -c

Authentication
--------------

Authentication is not required -- and can be shut off for a paste even once enabled -- but if you'd like to paste as yourself rather than anonymously, just setup your global git config like so:

    git config --global github.user "your-github-username"
    git config --global github.token "your-github-token"

You can find your GitHub username and token at https://github.com/account by clicking the 'Global Git Config' link.

Options
-------

- __-h__ or __--help__

Display the usage and exit.

- __-m__ or __--man__

Display the man page and exit.

- __-p__ or __--private__

Paste privately

- __-a__ or __--anonymous__

Do not use a username when posting.  This is the default when there is
no authentication information setup.

- __-n__ <name> or __--name__ <name>

Specifies the desired file name for data read from STDIN or the
clipboard.  When supplied along with files listed as arguments, the
<name> parameter will be given as the file name instead of the name of
the file as it exists on the system.

- __-t__ <type> or __--type__ <type>

Specifies the desired content type of the data pasted to Gist, either
via STDIN, the clipboard or file.  Gist will often ignore this
parameter in favor of guessing the type based on the file name.

- __-c__ or __--clipboard__

Reads and posts data from the clipboard via __pbpaste__ or __xclip__ if
available.

- __-o__ or __--open__

Open the URL in a browser once after pasting.  Supported via the
__open__ command (Mac OSX), or the __xdg-open__ command (Linux) if
either are available.

Examples
--------

Paste a single file

    gistpaste thatfile.txt

Paste multiple files of varying types

    gistpaste thatfile.txt Some.java another.pl

Paste a single file and override the name, all functionally equivalent.

    gistpaste --name=thatfile.diff thatfile.txt
    gistpaste --name=thatfile.diff < thatfile.txt
    cat thatfile.txt | gistpaste --name=thatfile.diff

Paste from STDIN

    grep "this" thatfile.txt | gistpaste
    svn diff thatfile.txt | gistpaste -t diff 
    gistpaste < thatfile.txt

Copy content to the system clipboard and paste it

    gistpaste -c
    gistpaste -c -t xml
    gistpaste -c -n mydata.xml

Paste a file without the name so Gist will not ignore the type
parameter

    gistpaste --name=" " -t diff thatfile.txt
    gistpaste -t diff < thatfile.txt
    cat thatfile.txt | gistpaste -t diff

Author
------

David Blevins <dblevins@visi.com>

