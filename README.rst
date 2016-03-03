Description
===========

Unurl transforms urls into temporary files

It is meant to quickly download files all thoses files that we only download
and use once before deleting them. As the same name is reused using it
repeatedly doesn't cumulate the sizes of everything downloaded in memory.

It returns a path to the file to stdout. This path is extension-less if no
extension could be found from the url, otherwise it tries to be smart and
puts it on the temp name to avoid breaking fragile programs.

Examples
========

::

    $ unurl 'https://istheinternetonfire.com/'
    /tmp/tmp-unurl

    $ cat `unurl https://istheinternetonfire.com/`
    < HTML bloat >

    # Without argument unurl returns the name so you don't have to redownload

    $ unurl
    /tmp/tmp-unurl

    $ grep '<P class' `unurl`
    <P class="yes">Yep.</P>
    <P class="maybe">Smoldering as usual.</P>
    <P class="yes">Yes!</P>

    # If an extension can be determined it will be used

    $ unurl http://i.imgur.com/KGDYTq9.gif
    /tmp/tmp_unurl.gif

    $ sxiv `unurl 'http://i.imgur.com/KGDYTq9.gif'`
    < Opens the gif with sxiv image viewer >


Warning
=======

Do not use unurl in scripts: as the filename is completely determined it
would be easy for an attacker to change its content between downloading and
using the file (temp-file attack).

(Granted, no attacker should be running wild on your system anyway but let's
not make their task easier...)

Documentation
=============

::

    Usage: unurl [-h] [-n name] [URL]

    Argument:
        URL     URL to download

    Options:
        -h, --help          Print this help and exit.
        -n, --name name     Use `name' as the temporary file name.

License
=======

This program is under the GPLv3 License.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.

Contact
=======

::

    Main developper: Cédric Picard
    Email:           cedric.picard@efrei.net
