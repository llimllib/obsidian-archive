https://v5.chriskrycho.com/essays/feeds-are-not-fit-for-gardening/

Lots to think about in here that's relevant to this site.

Currently I just [chuck the 15 most recent files](https://github.com/llimllib/obsidian_notes/blob/361d3717c4d63b5ce295e13045be420d99c58d84/run.py#L596-L603) that have changed, based on their git last modified timestamps, into the RSS feed and call it a day, but obviously a lot more thought and care could be put into it.

I'm thinking something like this would be a slight improvement:

- on creation, every file gets a created and modified date in the front matter
	- (I don't currently use front matter for anything)
- I only update the updated date on significant updates
- The RSS feed is the most recent N updates
- The front page has both a "new articles" and "recent updates" sections
	- the former is by created date
	- the latter is by modified date where modified != created

This doesn't address the issue that I've got three "blogs" on this site
- this link blog
- the "blog" blog where I write more article-ish things
- the music blog

And soon, I'm going to start publishing photos again, either here or on something like photos.billmill.org

Yet they don't each have a feed, so somebody can't subscribe to just what they're interested in.

(Do enough people read this that it's worth worrying about that?)

One possible route would be to generate a feed for each folder. Another would be to add the ability to add metadata to a folder indicating to the generator that the folder ought to have a feed, or to just add a `--feeds` flag to the generator that told it which folders to generate feeds for.

I think I'm going to do some experimenting with feed generation today and see what feels natural.