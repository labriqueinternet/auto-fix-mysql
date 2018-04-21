# Introduction

Du to MySQL being a stupid database that store it's core system database in the
MyISANE format, it regularly self corrupt itself on power failures thus making
it totally unusable.

Fixing this by hand it a long, painful, very complicated and horrible process.
This script is here to do that for you.

Sadly this process is not perfect and can fail for random reason but each part
of the script can be control individually to save your ass.

In theory it can also be run in a crontab in which it will backup the system
database for you and restore it from this backup instead of having to recreate
everything by hand but this has never been battle tested so use this
functionality at your own risks.

# Installation

Install requires:

    sudo apt-get update
    sudo apt-get install python-virtualenv python-dev rsync

Then:

    git clone https://github.com/labriqueinternet/auto-fix-mysql

    cd auto-fix-mysql

    virtualenv ve
    source ve/bin/activate

    pip install -U pip setuptools wheel
    pip install -r requirements.txt

# Usage

The simple usage is:

    source ve/bin/activate
    python auto-fix-mysql

This will follow this execution scheme:

* is MySQL is broken? No, then do a backup
* else, try to fix mysql
* do I have a backup? Yes, then restore it
* otherwise, start the manual fix procedure

If any step failed, you can run them manually, here is the help page:

    usage: auto-fix-mysql [-h]
                          {backup-mysql-db,fix-mysql,fix-mysql-manually,fix-mysql-using-backup,get-user-schema,launch-mysql-in-safe-mode,mysql-is-broken,mysql-is-running,recreate-apps-users,recreate-broken-system-tables,stop-mysql,there-is-a-backup}
                          ...

    positional arguments:
      {backup-mysql-db,fix-mysql,fix-mysql-manually,fix-mysql-using-backup,get-user-schema,launch-mysql-in-safe-mode,mysql-is-broken,mysql-is-running,recreate-apps-users,recreate-broken-system-tables,stop-mysql,there-is-a-backup}
        backup-mysql-db
        fix-mysql
        fix-mysql-manually
        fix-mysql-using-backup
        get-user-schema
        launch-mysql-in-safe-mode
        mysql-is-broken
        mysql-is-running
        recreate-apps-users
        recreate-broken-system-tables
        stop-mysql
        there-is-a-backup

    optional arguments:
      -h, --help            show this help message and exit

The manual fix part matched to follow commands call:

    python auto-fix-mysql recreate-broken-system-tables
    python auto-fix-mysql stop-mysql
    python auto-fix-mysql recreate-apps-users

This "step by step" called are pretty new and not well tested, ping Bram if
things don't work as expected.
