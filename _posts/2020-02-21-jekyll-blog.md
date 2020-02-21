## What is Jekyll
Jekyll is a static site generator built to handle blog posts out of the box. It uses Markdown for content allowing us to write rich blog posts using Markdown. Because of this it is trivial to get a basic blog up and running quickly. However the the [Liquid HTML templating engine](https://github.com/Shopify/liquid/wiki) allows us to build complex themes. 

## Why use Jekyll & Github Pages
Because GitHub is made for collaboration it provides an ideal platform for hosting a shared blog. Anyone with access to the repository can submit changes using a pull request and we can use the existing Github workflow to approve changes.

Github also has inbuilt Jekyll integration because Github pages uses Jekyll default and can automatically build your site when you commit.


## Getting started

### What you need
Jekyll is a ruby application and so you will need a [ruby development environment](https://jekyllrb.com/docs/installation/) setup.

You can then install the jekyll and bundler gems
```sh
gem install jekyll bundler
```

If you do not have permissions to write to your gems directory you can grant yourself access to the directory or use a tool like RVM or rbenv to manage your Ruby environment.

### Create your site
The Jekyll command will create a new site for you.
```sh
jekyll new myblog
```
This command creates the myblog directory for you. 


### If bundle install fails
As previously mentioned, you may find RVM or rbenv useful to manage your environment. As an alternative, if, on the next step you get errors installing your application dependencies then you can install them locally with the following command.
```sh
bundle config set path 'vendor/bundle'
echo .bundle >> .gitignore
```

### Build and run your site
Make sure you are in your site directory and run the bundle command to build and serve a development version of your blog.
```sh
cd myblog
bundle exec jekyll serve
```
Now you can browse to http://localhost:4000 and see your blog.


## The jekyll directory structure
Before we start modifying our site we'll take a moment to get familar with the Jekyll files and directories.

### Configuration file
The `_config.yml` file contains your site configuration. This is where you can define global settings, define your theme and install plugins. You don't need to change anything in there for a basic site.

### Pages
Any markdown files in your root directory will be rendered as pages. The default theme will show these in the site navigation at the top right. Don't worry about the file extensions, .markdown and .md both work for markdown files.

#### Activity
Open about.markdown and note the section at the top
```md
---
layout: page
title: About
---

```

This section, called `front matter` contains the configuration for the site. It it specified between lines of `---`. The rest of the page is plain markdown. Note that you don't need to add the page title as the theme will automatically inject the title from the page front matter. Try editing the markdown to include a description of your page.

Now let's make a new page. Copy the file about.markdown to contact.md and open it in your editor.
* Change the title to Contact and the permalink to /contact/. Enter some contact information in the markdown body.
* Reload your page and navigate to the new contact page


### Blog Posts
Blog posts are created in the \_posts directory. By default, posts in the future will not appear (unless you set them to in the \_config.yml file).
* Create the new file `_posts/2020-02-14-first-post.md` and open it in your editor
* Enter the following front matter in your file
```md
layout: post
title: 'First post'
date: '2020-02-14 10:48:00 +0930'
categories: announcements
```

Now type your first blog post after the front matter and reload your page

Congratuations you have a blog!



## Theming
So far we've been using the default theme. There are a whole lot of [different themes](http://jekyllthemes.org/) to choose from. To switch to an alternate theme you can use bundler to install the theme and set the theme in your \_config.yml file.
```
bundler add jekyll-theme-minimal
```
However if you want something a bit more custom you can override the theme with your own styles and page layouts. The easiest way to do this is to override (or augment) the existing theme by adding your designs to the `_layouts` directory.


### Copy files from your theme
You can write these files from scratch but it is easier to get started with an existing theme. The default Jekyll theme `minima` is a nice clean place to start. So I'm going to copy files from the installed minima theme to get started however if you want to start with a different theme you can copy from that.


First I'm going to get the path to my theme and have a look inside
```bash
$> bundler info minima
  * minima (2.5.1)
	Summary: A beautiful, minimal theme for Jekyll.
	Homepage: https://github.com/jekyll/minima
	Path: /var/www/html/projects/tmp/mygallery/vendor/bundle/ruby/2.5.0/gems/minima-2.5.1
$> ls /var/www/html/projects/tmp/mygallery/vendor/bundle/ruby/2.5.0/gems/minima-2.5.1
	assets/  _includes/  _layouts/  LICENSE.txt  README.md  _sass/

```
Running `bundler info` providers us with details for an installed gem. Here we can get the path that tells us where the gem in installed. Use this directory to find your theme data. 

To override a theme we can place alternate theme files in our site directory. Jekyll will first look in your site and then look in your theme directory so you can override only the sections that you require.
For the sake of this exercise lets copy all this data over to our site (although in practice it would be better to only copy those that we need). Note that I am using the directory from the `bundler info` command earlier.
```
$> cp -r vendor/bundle/ruby/2.5.0/gems/minima-2.5.1/_* .
```

### Edit your theme
Open `_layouts/default.html` to get the default theme that is currently loaded on each page. Jekyll uses a language called liquid to create page templates. As you can see, it looks just like HTML exccept for some special tags.


#### Objects
```
{{ site.title }}
```
Two curly braces tells liquid to output the content into the page. This examples writes the site title. 


#### Tags
Content in `{%` and `%}` tags are used for logic.
```
{% if site.author %}
	{{ site.author }}
{% endif %}
```
This example will show the author only if the author is set.


#### Includes
We can load smaller pieces of content using includes. Our includes are liquid HTML files in the `_includes` directory. These can be in either your site or in your theme directory.
```
{%- include footer.html -%}
```
The above line imports the content from `_includes/footer.html`.


#### Filters
Data can be run through a fitler before it is output. We pass data to a filter by using a `|` symbol.
```
{{ site.title | escape }}
```
The above line uses the [escape](https://shopify.github.io/liquid/filters/escape/) filter which will replace characters with HTML escape sequences.


### Remove the footer
We've already created a page of contact information so we don't need it in the footer anymore. Let's take it out. Remove the following line from `_layouts/default.html`
```
{%- include footer.html -%}
```
Now reload your page and the footer is gone!



### Get your style on
You can edit the stylesheets by modifying the sass files in `_sass`. So with that in mind, lets change our blog list to a card list similar to [many example blog designs](https://www.google.com/search?tbm=isch&q=blog+design) online.


First edit the markup by modifying `_layouts/home.html` to reflect the following. Notice how we access the post varibles through the site.posts array.
```md
---
layout: default
---

<div class="home">
	{%- if page.title -%}
		<h1 class="page-heading">{{ page.title }}</h1>
	{%- endif -%}

	{{ content }}

	{%- if site.posts.size > 0 -%}
		<h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>
		<div class="post__list">
			{%- for post in site.posts -%}
			<a class="post__preview" href="{{ post.url | relative_url }}">
				<figure class="post__image">
					{%- if post.image -%}
						<img src="{{post.image}}" alt="{{post.image_caption}}" />
					{%- else -%}
						<img src="https://via.placeholder.com/300x200" alt="Placeholder image" >
					{%- endif -%}
				</figure>
							
				<div class="post__body">
					{%- if post.categories.size-%}
						<ul class="post__categories">
							{%- for category in post.categories -%}
								<li>{{category}}</li>
							{%- endfor -%}
						</ul>
					{%- endif -%}
					<h3 class="post__title">{{ post.title | escape }}</h3>
				</div>
				<div class="post__details">
					<span class="post__date">{{ post.date | date: "%a, %b %d, %y" }}</span>
				</div>
			</a>
			{%- endfor -%}
		</div>

		<p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
	{%- endif -%}

</div>
```


Now lets style it. To keep things clean we will create the new file `_sass/_posts.scss` and enter the following
```sass
.post {
	&__list {
		display: flex;
	}

	&__preview {
		display: flex;
		flex-direction: column;
		text-decoration: none;
		margin: 5px 10px 25px;
		background: #f1f3f5;
		border-radius: 5px;
		color: #405261;
		overflow: hidden;

		&:hover,
		&:visited {
			text-decoration: none;
			color: #405261;
		}

	}

	&__image {
		margin: 0;
	}

	&__body {
		padding: 30px;

		> * {
			margin: 0;
			text-align: center;
		}
	}

	&__categories {
		list-style-type: none;
		display: flex;
		align-items: center;
		justify-content: center;

		li {
			padding: 5px;
			color: #93a1b0;
			letter-spacing: .75px;
			margin-bottom: 2px;
			text-transform: uppercase;
		}
	}

	&__title {
		font-size: 1.6rem;
	}

	&__details {
		padding: 0 5px 5px;
	}

	&__date {
		color: #79818a;
	}
}
```


Finally include your styles in the existing minima stylesheet by adding your new file to the imports in `_sass/minima.scss` as below
```sass
// Import partials.
@import
  "minima/base",
  "minima/layout",
  "minima/syntax-highlighting",
	"posts"
;
```


Now reload your page and you have a rather common card style (including the poor colour contrast)


Because we use the `post.image` property, you can now add an image to your posts by adding the image attribute to your posts front matter
```
image: https://upload.wikimedia.org/wikipedia/commons/4/42/Jekyll_%28software%29_Logo.png
```
