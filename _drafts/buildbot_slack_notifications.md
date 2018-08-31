---
title: (buildbot/slack) Add slack notifications to buildbot
dropcaps: false
published: false
draft: true
tags:
- devops
- buildbot
- slack
---
Create custom emojis for each builder.
Highjack the HttpStatusPush

~~~python
sp = reporters.HttpStatusPush(serverUrl=SLACK_TECH_URL, format_fn=edit_build_infos,
    wantProperties=True, wantPreviousBuild=True)
~~~

Insert some logic to pick appropriate emoji for state changes, ie when the build got broken/repaired. 

~~~python
def edit_build_infos(build):
    """We take advantage of this callback to grab the infos we need from the build dict,
       compute other infos we need and send payload to slack.
       Return None to end default HttpStatusPush behaviour prematurely.
    """
    if (not build['results'] and not build['prev_build']['results']):
        return  # Still OK, nothing to see...

    # Grab infos from git
    rev = build['properties']['got_revision'][0]
    build_dir = os.path.join(build['properties']['builddir'][0], 'build')
    commit_infos = subprocess.check_output(['git', 'log', '-n', '1', '--pretty=format:"%an|%s"', rev], cwd=build_dir)
    author = commit_infos.split('|')[0].split(' ')[0][1:]
    commit_msg = ' '.join(commit_infos.split('|')[1:])  # join in case there were '|' in commit msg
    details = '`%s` by %s' % (commit_msg, author.lower())

    msg = '<%s|#%s>: %s' % (build['url'], build['number'], details)

    title = "Buildbot '%s'" % build['builder']['name']
    if not build['results']:
        if build['prev_build']['results']:  
            msg = ':white_check_mark: ' + msg  # build repaired
    elif 'prev_build' not in build or not build['prev_build']['results']:
        msg = ':poison: ' + msg    # build just got broken
    else: 
        msg = ':no_entry: ' + msg  # build still broken
        
    if msg:
        requests.post(SLACK_CHANNEL[build['builder']['name']],
                      {'payload': json.dumps({
                          'text': msg,
                          'username': title,
                          'icon_emoji': ':build-%s:' % build['properties']['branch'][0]}
                      )}, verify=False)
~~~
