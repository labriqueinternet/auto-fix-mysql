Install requires:

    sudo apt-get update
    sudo apt-get install python-virtualenv python-dev rsync

Then:

    virtualenv ve
    source ve/bin/activate

    pip install -U pip setuptools wheel
    pip install -r requirements.txt

To run:

    source ve/bin/activate
    python auto-fix-mysql

It should be in a crontab something like every hour but this is not battle tested yet.
