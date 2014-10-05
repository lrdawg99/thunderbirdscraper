#!/usr/bin/env python
#
# Extracts email addresses from one or more plain text files.
#
# Notes:
# - Does not save to file (pipe the output to a file if you want it saved).
# - Does not check for duplicates (which can easily be done in the terminal).
#
# (c) 2013  Dennis Ideler <ideler.dennis@gmail.com>

from optparse import OptionParser
import os.path
import re

regex = re.compile(("([a-z0-9!#$%&'*+\/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+\/=?^_`"
                    "{|}~-]+)*(@|\sat\s)(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?(\.|"
                    "\sdot\s))+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?)"))

def file_to_str(filename):
    """Returns the contents of filename as a string."""
    with open(filename) as f:
        return f.read().lower() # Case is lowered to prevent regex mismatches.

def get_emails(s):
    """Returns an iterator of matched emails found in string s."""
    # Removing lines that start with '//' because the regular expression
    # mistakenly matches patterns like 'http://foo@bar.com' as '//foo@bar.com'.
    return (email[0] for email in re.findall(regex, s) if not email[0].startswith('//'))

if __name__ == '__main__':
    parser = OptionParser(usage="Usage: python %prog [FILE]...")
    # No options added yet. Add them here if you ever need them.
    options, args = parser.parse_args()

    if not args:
        parser.print_usage()
        exit(1)
    
    out = ''
    for arg in args:
        if os.path.isfile(arg):
            print 'First Name,Last Name,Display Name,Nickname,Primary Email,Secondary Email,Screen Name,Work Phone,Home Phone,Fax Number,Pager Number,Mobile Number,Home Address,Home Address 2,Home City,Home State,Home ZipCode,Home Country,Work Address,Work Address 2,Work City,Work State,Work ZipCode,Work Country,Job Title,Department,Organization,Web Page 1,Web Page 2,Birth Year,Birth Month,Birth Day,Custom 1,Custom 2,Custom 3,Custom 4,Notes,'
            for email in get_emails(file_to_str(arg)):
                out+= ',,,,'                
                out+= email
                out+= ',,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,\n'
            email.replace(" ", "").replace("\t", ""),
            print out
        else:
            print '"{}" is not a file.'.format(arg)
            parser.print_usage()