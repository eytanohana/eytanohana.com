---
title: How I accidentally broke Production for 2 weeks
description: How I accidentally broke Production for 2 weeks
---

# How I accidentally broke Production for 2 weeks

*February 8, 2026*

<figure markdown="span">
    ![Servers on Fire](../../assets/blog/servers-on-fire.png)
</figure>

Yes, I broke production, no I didn't mean to, here's how.

## The Deployment Process

On a team I previously worked on, for a specific repository, we had our own custom deployment process out of the norm
from the rest of the company. The repo itself was a legacy repo where whenever we merged a new feature to master
we would manually run a deploy script. This would then take the latest changes in master in our repo and
push it to a different repo, considered "production" and finally the latest master in the "prod" repo would be zipped up
and stored in an S3 bucket. Later, when a service was running in production that needed the latest changes, it would
manually download and extract the repo from S3 and insert it into the PHYTHONPATH for the service to use.

## The Backstory

Both repositories originally existed in BitBucket. Around the time I joined the company, a dev who was leaving the
team for a different role in the company was tasked with finally migrating the repository to GitHub. What we didn't know
in that migration was that the deployment now relied on a single ssh key in the dev's GitHub account. So for years we all
went along making changes and deploying new features without a hiccup.

Throughout that time, I would talk to this dev back-and-forth. He would reach out to me for help; I would reach out to him.
One day in these calls, I kept noticing every time he would push a change to his own repo on his team, he would have to manually
enter his username and password for the push. So one day I finally said, "hey I can help you set up your git so you don't need to do that on every push".

He agreed and we spent the next 10 minutes setting up ssh keys in his GitHub account. That's when we found some old pre-existing ssh key
already stored in his account but we both weren't sure what it was for. So I made the mistake in saying "OK you have some old
key in your account already, let's be safe and just remove it to start clean". We removed the key, and added his new one.
He was now able to push without needing to manually insert his credentials each time. He said thanks; I said "no problem!" and we all moved on.

## What Happened Next
