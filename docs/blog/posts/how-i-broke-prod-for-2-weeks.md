---
title: How I Accidentally Broke Production for 2 Weeks
description: How a small, well-intentioned change quietly broke our deployment pipeline
---

# How I Accidentally Broke Production for 2 Weeks

*February 8, 2026*

<figure markdown="span">
    ![Servers on Fire](../../assets/blog/servers-on-fire.png)
</figure>

>Yes, I broke production. No, I didn't mean to. Here's how.

## A Rickety Pipeline

On a team I previously worked on, one repository we worked on had a custom deployment process that differed from the rest of the company.

It was a legacy setup. Whenever we merged a feature into `master`, we manually ran a deploy script that launched a jenkins CI/CD pipeline that would:

1. Take the latest `master` from the **development repository**
2. Push it into a separate **production repository**
3. Zip the production repository
4. Upload the archive to an S3 bucket

When a service running in production needed the latest code, it would download the archive from S3, extract it, and add it to its `PYTHONPATH`.

It wasn't elegant, but it had been working for years.

## An Innocent Favor

Both repositories originally lived in Bitbucket. Around the time I joined the company, a dev on the team who was soon transitioning to another role was tasked with migrating them to GitHub.

What we didn't realize during that migration was that the deployment pipeline now relied on a **single SSH key** tied to that developer's GitHub account.

For years, everything worked. We merged features, ran deployments, and never questioned it.

I stayed in touch with the dev after he moved teams. We'd help each other out from time to time, and I always noticed during our calls that every
time he pushed code to his new team's repos, Git would prompt him for his username and password.

Eventually I offered to help him configure SSH keys for his account so he wouldn't have to go through that anymore.

He agreed, and we spent about ten minutes configuring the keys on his machine and GitHub account. While doing that, we noticed
an **old SSH key** already present on his account. Neither of us recognized it or remembered what it was for.

And here's the mistake. I said, "Ehh it's an old key. You can probably remove it and just start clean."

We deleted it, added the new key, and everything worked. He could push without entering credentials. We both moved on.

## The Silent Break

Nothing broke immediately. No alerts fired. No deployments failed. Everything looked normal.

Until a couple of weeks later, a project manager came to the team and said a customer was complaining: a feature we had "deployed" the previous week didn't seem to be working.

The first thing I did was check the logs. Nothing stood out. No errors related to the new feature.

Next, I checked the Jenkins pipeline for that deployment. Every step was green. The pipeline had passed.

Then I checked the production repository on GitHub.

The last commit was over **two weeks old**.

That made no sense. We were redeploying multiple times a week.

So I went back to Jenkins and started opening individual steps—each one still marked as successful. When I opened the step responsible for pushing code
from the dev repo to the prod repo, I finally saw it: **"Failed pushing to Prod Repo."**

Jenkins had failed to push the code… but continued the pipeline anyway.

It zipped the old code.  
Uploaded it to S3.  
And marked the deployment as successful.

Every deployment for the past two weeks had been packaging and redeploying stale code and thankfully only one customer had noticed so far.

## The Fix

Once we realized what had happened, the fix was simple.

The deployment pipeline had been using the SSH key we deleted from that developer's GitHub account.

I generated a new SSH key in my own account, added the public key to GitHub, and updated the pipeline.

Deployments started working immediately.

---

This wasn't a story about a bad deployment system, or a bad engineer.

It was a story about hidden coupling, silent failure, and how a small, well-intentioned cleanup can ripple through a system in unexpected ways.
