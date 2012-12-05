moodle-mysql-munin
==================

This provides some performance statistics for Moodle 2
using the standard 'munin' tool.

installation
============

Place the 'moodle_' file in a convenient location but
not in your munin plugins folder. 

In your plugins folder symlink the 'moodle_' file to a
file called moodle_yourdatabase where the 'yourdatabase'
part is the name of your Moodle 2 database. The script
infers the database name from the filename. If you have multiple
Moodle 2 sites you can perform multiple symlinks with different
database names. 

Example: in Ubuntu, it would be something like

    sudo
    cd /etc/munin/plugins
    ln -s /usr/share/munin/plugins/moodle_ moodle_moodle2

...assumes you placed the file in /usr/share/munin/plugins and
your Moodle database is called 'moodle2'.

configuration
=============

In your munin-node plugins configuration file (on Ubuntu this is

    /etc/munin/plugin-conf.d/munin-node

), create a new section for moodle_ as follows:

    [moodle_*]
    env.hostname localhost
    env.user moodleuser
    env.password moodlepass
    env.turnitin 1

...substituting the appropriate details for your site. Remember that
the database name is extracted from the symlink name (see above). If you
don't use turnitin set that to 0.

'''Restart munin-node''' (see local documentation)

testing
=======

You can test as follows...

    munin-run moodle_database

(substitute the name you used). This should produce something like...

    multigraph users
    users.value 15
    logins.value 8
    multigraph logs
    logentry.value 78
    multigraph courses
    numcourses.value 160
    numvisible.value 134
    multigraph activities
    turnitinsubmission.value 0
    assignsubmission.value 0
    quizattempts.value 1
    forumposts.value 0


