---
title:  "How I created my first coding blog"
date:   2020-12-25 13:37:00 +0100
categories: blog coding jekyll
tags: blog coding jekyll minima first
---

## The Initial Situation
So I decided that I want to write a tech blog. I thought it might be a good idea to document some of the things I stumble upon in my day job and maybe have people comment on them so that I may even do stuff better in the future. So all I need is a blog, where I can share all my extremely important insights. But how do I start?

To be honest, I don't have too much experience writing HTML, CSS and Javascript. I played around with a Ruby on Rails project - like, five years ago - but apart from some basics, not a lot stuck with me. And it also seemed overly complicated to create a Ruby on Rails project or an ASP.Net Core App just to wirte a blog.

So those initial thoughts out of the way, I did the sane thing: I googled. And I stumbled upon a suspiciously high amount of websites and blogs telling me *'Just use Wordpress and BlueHost, and, hey, while we're at it, here is an affiliate link so that you get 10% off'*. After wondering for a moment if I maybe really needed to spend at least 80€ a year up front for having a blog, I took a moment to reconsider what I **really** needed and came up with the following requirements:

- My blog should not cost me a lot[^1].
- It should be really quick to set up, so that I can start to blog as quickly as possible.
- I should not have to worry about <abbr title="Search Engine Optimization">SEO</abbr>, mobile experience or other web-development stuff - it just needs to work. But at the same time it obviously shouldn't look too shabby.

## My Solution (In Short)
I decided to use [Jekyll](https://jekyllrb.com/) in combination with the [Minima-Theme](https://github.com/jekyll/minima) and host it on Github-Pages. Using the very helpful [Step-By-Step-Guide](https://jekyllrb.com/docs/step-by-step/01-setup/) I had a blog up and running in no time. Using Github, you have the additional benefit of a kind of built-in CI/CD toolchain, which automatically takes your commited source code, basically runs <code>jekyll build</code> and hosts the result. Also, it's pretty cool to blog using markdown (make sure to talk about it a lot for extra street credibility ;))

## My Solution (Lengthy)
### Static Site Generators
After some digging I stumbled across many posts recommending [Gatsby](https://www.gatsbyjs.com/). Gatsby is an example of a static site generator - these allow you to quickly create static websites, getting rid of a lot of the overhead usually involved in writing plain html. 

Static Site Generators are frameworks that translate content and layout files into full-blown html-sites. The separation between content and layout allows for a simple usage of third-party themes for your websites. So it's pretty easy to build a visually appealing website or to change themes later on. Moreover there often exist plugins for many different use cases: Perform Search Engine Optimization for the generated HTML, offer RSS feeds for your page, and so on. The content may often be written in markdown and template languages such as [Liquid](https://shopify.github.io/liquid/) or [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), which makes creating webpages quite enjoyable[^2]. The advantages of a static website are pretty clear:
- It's fast.
- It's very cheap to host (or hosting may even be for free - see the Hosting section).
- You don't have to worry too much about security.

But having only static webpages is of course quite restrictive - it will simply not be possible to provide dynamic content, have user logins or more generally have any kind of database interaction. But since I want to create a blog where only I can write posts and where I don't need any kind of LogIn mechanisms or API-calls, these restrictions don't limit me. A potential problem is the ability of readers to comment my content, but platforms like [Disqus](https://disqus.com/profile/login/) make it easy to implement this in your static site.

I ended up using [Jekyll](https://jekyllrb.com/) -  I found it really straightforward and simple to use and I have a special place in my heart for everything written in Ruby. Moreover, it's designed to make blogging really easy.

### Hosting
Having decided that I want to blog using static pages, I next checked the hosting options. Just googling it you'll find lots of great results and notice how hosting will cost you next to nothing. I haven't tried it, but [Netlify](https://www.netlify.com/) sounds like a great place to start, as it offers an integrated CI/CD toolchain for many Static Site Generators. That means that you can connect your Netlify hosted site to your repository (i.e. GitHub, GitLab, ...) and after pushing the changes to your Gatsby, Jekyll, Hugo,... project, Netlify will take care of building and automatically deploying those changes.

Having decided to use Jekyll, there is another, even easier solution to host the blog (or website): You can use Github Pages - a hosting service by Github, which natively supports Jekyll projects. More specifically, as with Netlify, you can just push the changes made to your Jekyll project (i.e. new blog posts) to a specific repository in you github account and they will be published on your custom Github-Pages domain. Read this [article](https://guides.github.com/features/pages/) to set up a basic Github-Pages project using Jekyll and the Github Theme Chooser in about 5 minutes.
The biggest advantage: per Github account one personal Github-Pages Webpage is hosted for free - so I don't have to pay anything to get my blog hosted.  

### Blogging
As there is no database used, all blog posts are stored as either plain html or markdown. The advantage of this is that you can simply commit your new posts, assets and other changes to your Source Control Management (probably Git), push it to some remote and work on your blog from anywhere and any system.

Happy blogging!

## Footnotes
[^1]: I really get that you can also see a blog as an investment in yourself and that you can even monetize it. But a) I don't want to monetize my blog and b) I realistically don't know for how long I will be blogging or if I will have fun blogging regularly - so I don't want to have a big commitment. And also c) I still got a bit of nostalgia for the *old* internet, where you could simply host static sites for virtually no money.
[^2]: You have to get used to the conventions of a new network. But probably, if you already have some experience in HTML, CSS and JavaScript, this process will not take long.
