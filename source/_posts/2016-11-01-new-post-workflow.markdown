---
layout: post
title: "New Post Workflow"
date: 2016-11-01 10:54:43 -0400
comments: true
categories: personal
---

The main problem is that I want to have the source code of this blog in multiple places so I can add posts both at home and at work without to much trouble. I also have an EC2 instance where I host the blog, so all three places need to have the same up to date versions of the blog at all times. Git to the rescue! 

## Creating a new post and pushing to Github

1. Create the blog post in MS Word.
+ Run the built in rake command to generate a file in your posts directory /path/to/your/blog/source/_posts/

{% codeblock %} 
rake new_post["title"]
{% endcodeblock %}

The “new_post” rake task takes one “Title” argument. This will, wait for it, be the title of your new post. The name of the file will include the current date followed by the title. Following our structure this will be the full path of this post:
{% codeblock %} 
/octopressblog/source/_posts/2016-11-01-new-post-workflow.markdown
{% endcodeblock %}
+ The following code block includes all the commands to add, commit and push the newly created post to the master git repository. I use GitHub, but these commands will work for any personal BitBucket or similar. 

{% codeblock %} 
git add .
git commit –m “Created post: 2016-11-01-new-post-workflow.markdown”
git push -u origin Macbook
{% endcodeblock %}


## Pulling the new changes to the EC2 instance

Now that we have a new post that’s pushed up to Github, lets pull it down to the EC2 instance and regenerated Octopress to reflect our changes.

1. Using git pull the changes:
{% codeblock %} 
git pull origin Macbook
{% endcodeblock %}
+ Use the rake task to generate posts and pages into the public directory
{% codeblock %} 
rake generate
{% endcodeblock %}
+ Restart apache to reflect the changes
{% codeblock %} 
sudo service apache2 restart
{% endcodeblock %}

