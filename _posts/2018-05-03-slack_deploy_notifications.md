---
title: Creative use of <code>git blame</code> for slack deploys notifications
description: Slack changelog notification displaying author face for each item in the changelog
dropcaps: true
published: true
comments: https://www.reddit.com/r/Slack/comments/8gu3ja/creative_use_of_git_blame_for_slack_deploys/
tags:
- git
- slack
- python
---

The goal is to make explicit who coded a deployed feature so that people (outside the dev team) know who to contact in case of complaints or praises.

{:.center}
![slack notification with developers facemojis](/public/img/posts/slack_deploy_notif.png)  
*Slack deploy notification with authors faces*

This technique requires to have facemojis named after each developer (4 first letters of firstnames).
It relies on a `develop.md` file that contains the changelog of the upcoming release, like so :

~~~~markdown
Higher level release description 

### Added 
- item 1 

### Fixed
- item 2
- item 3
~~~~

We parse the output of `git blame` on that file to prepend a developer facemoji for each item.  

For example, imagine I've coded item 1 feature and added it to the `develop.md`, then line `- item 1` becomes `:fabr: item 1`.  
 
Code is straight-forward :

~~~~python
def get_changelog(changelog_path):
    """Extract release synopsis and changelog from given file.
    """
    blamelog = subprocess.check_output('git blame %s' % changelog_path)
    synopsis = []
    changelog = []
    h3_found = False
    for blameline in blamelog.split('\n'):
        line = ''.join(blameline.split(') ')[1:])
        if line.startswith('###'):
            h3_found = True
        if not h3_found:
            synopsis.append(line)
        else:
            if line.startswith('- '):
                author = blameline.split()[1][1:5].lower()
                line = ':%s: %s' % (author.lower(), line[2:])
            changelog.append(line)
    return synopsis, changelog
~~~~

We're done, you can craft a message with the synopsis and changelog and post a slack notification using 
[requests](http://docs.python-requests.org/en/master/).

Obviously, for this trick to work, each developer must log his activity in `develop.md` and one should avoid at all costs editing others lines or the output of `git blame` won't reflect original authors.
