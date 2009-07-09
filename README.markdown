[[meta title="__gistpaste__ - Command line paste script for gist.github.com"]]
[[meta author="David Blevins <david.blevins@visi.com>"]]

Gistpaste: Command line paste script
====================================

This script can do all that the "defunkt/gist" script can, plus it can
post multiple files, post clipboard output, post anonymously even if a
global git config exists, specify file name, or specify file type.  I
would have fixed that script, but I don't know Ruby (sorry defunkt!).

This script cannot "read" gists like the "defunkt/gist" script can.  I
plan to create a gistcopy script for that at some point.

# INSTALLATION

Download and install

  wget http://github.com/dblevins/gistpaste/raw/master/gistpaste &&
  chmod 755 gistpaste &&
  sudo mv gistpaste /usr/local/bin/

Add any Perl modules you may not have

  sudo cpan install LWP::UserAgent
  sudo cpan install File::Which

# NAME

__gistpaste__ - Command line paste script for gist.github.com

# SYNOPSIS

__gistpaste__ [options] [FILE...]

- Paste file(s)

gistpaste thatfile.txt another.diff

- Paste STDIN

grep "this" thatfile.txt | gistpaste
 

- Paste the clipboard contents

gistpaste -c

# DESCRIPTION

Pastes content to gist.github.com, a fullly featured paste bin.
Resulting paste URL is printed to STDOUT and coppied to clipboard.
Pastes can be generated from files, STDIN and the system clipboard.
Clipboard support relies on either __pbpaste__ or __xclip__.

Pastes may be done anonymously or authenticated.  See the
gist.github.com account page at <https://github.com/account> and
click the 'Global Git Config' for instructions on how to setup

# OPTIONS

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

# PREREQUISITES

The `LWP::UserAgent` and `File::Which` modules are required.

 sudo cpan install LWP::UserAgent
 sudo cpan install File::Which

# EXAMPLES

Paste a single file

  % gistpaste thatfile.txt

Paste multiple files of varying types

  % gistpaste thatfile.txt Some.java another.pl

Paste a single file and override the name, all functionally equivalent.

  % gistpaste --name=thatfile.diff thatfile.txt
  % gistpaste --name=thatfile.diff < thatfile.txt
  % cat thatfile.txt | gistpaste --name=thatfile.diff

Paste from STDIN

  % grep "this" thatfile.txt | gistpaste
  % svn diff thatfile.txt | gistpaste -t diff 
  % gistpaste < thatfile.txt

Copy content to the system clipboard and paste it

  % gistpaste -c
  % gistpaste -c -t xml
  % gistpaste -c -n mydata.xml

Paste a file without the name so Gist will not ignore the type
parameter

  % gistpaste --name=" " -t diff thatfile.txt
  % gistpaste -t diff < thatfile.txt
  % cat thatfile.txt | gistpaste -t diff

# AUTHOR

David Blevins <david.blevins@visi.com>

