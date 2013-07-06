---
layout: post
title: "Octopress experience"
date: 2013-07-03 23:50
comments: true
categories:
published: false
---

> In this post I'll be explaning why and how I'm using octopress in this site, maybe it will help someone but mainly it will help me remember the process and changes in the future.

It took me over a month to slowly understand what octopress is and what was the best option for me to install and deploy it.

Finally I chose Github Pages...

Install

Theming

Tweaking

Other modifications:



Home page Keywords and Description

The Octopress by default shows latest post as home page, I choose not to go this way, my default home page is archive list. So there is no post from where it should include the keywords and description.

Setting Keywords and Description for Home page in _config.yml

Open the _config.yml and add the kewords and description keys:

description: Kornelije Sajler (xajler) Learn-a-holic Geek Notes. Human compiled Brainwork by Kornelije Sajler (xajler).
keywords: Kornelije Sajler, xajler, metaintellect, learnaholic, learn-a-holic, coding, programming, Ruby, Ruby On Rails, RSpec TDD, cucumber, jasmine, bacbone.js, postgresql, mongodb
Change head.html template to be aware of Home page SEO

In .themes/classic/source/_includes/head.html after meta tag for author replace the current description/keywords code with this one:

<meta name="author" content="{{ site.author }}">
{% capture description %}{% if page.description %}{{ page.description }}{% elsif site.description %}{{ site.description }}{%else%}{{ content | raw_content }}{% endif %}{% endcapture %}
<meta name="description" content="{{ description | strip_html | condense_spaces | truncate:150 }}">
{% if page.keywords %}<meta name="keywords" content="{{ page.keywords }}">{%else%}<meta name="keywords" content="{{ site.keywords }}">{% endif %}




Rakefile:

some seen here http://www.ewal.net/2012/09/08/octopress-customizations/

Just after the line ' post.puts "categories: " '
{% codeblock Set new post as draft, add desc and keys, and open on Subl - Rakefile %}

    post.puts "published: false"
    post.puts "description: "
    post.puts "keywords: "
    post.puts "---"
  end
    system "subl \"#{filename}\""
end
{% endcodeblock %}


{% codeblock Rake x to just quickly update - Rakefile %}
desc "Generate website, add, commit and deploy"
task :x do
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -am \"#{message}\""
    #Rake::Task[:integrate].execute
    Rake::Task[:generate].execute
    system "git push origin source"
    Rake::Task[:deploy].execute
end
{% endcodeblock %}

{% codeblock Update sitemap and notifications Rakefile %}
desc 'Notify Google of the new sitemap'
task :sitemapgoogle do
  begin
    require 'net/http'
    require 'uri'
    puts '* Pinging Google about our sitemap'
    Net::HTTP.get('www.google.com', '/webmasters/tools/ping?sitemap=' + URI.escape('http://www.ewal.net/sitemap.xml'))
  rescue LoadError
    puts '! Could not ping Google about our sitemap, because Net::HTTP or URI could not be found.'
  end
end

desc "Notify various services about new content"
task :notify => [:sitemapgoogle] do
end
{% endcodeblock %}

{% codeblock Rename post with the correct date (Will improve for the title too??) Rakefile %}
desc "Rename files in the posts directory if the filename does not match the post date in the YAML front matter"
task :rename_posts do
  Dir.chdir("#{source_dir}/#{posts_dir}") do
    Dir['*.markdown'].each do |post|
      post_date = ""
      File.open( post ) do |f|
        f.grep( /^date: / ) do |line|
          post_date = line.gsub(/date: /, "").gsub(/\s.*$/, "")
          break
        end
      end
      post_title = post.to_s.gsub(/\d{4}-\d{2}-\d{2}/, "")  # Get the post title from the currently processed post
      new_post_name = post_date + post_title # determing the correct filename
      is_draft = false
      File.open( post ) do |f|
          f.grep( /^published: false/ ) do |line|
            is_draft = true
            break
          end
      end
      if !is_draft && post != new_post_name
          puts "renaming #{post} to #{new_post_name}"
          FileUtils.mv(post, new_post_name)
      end
    end
  end
end
{% endcodeblock %}

{% codeblock Dont know if this one works.. should look it up Rakefile %}

desc "Publish draft"
task :publish_draft do
  posts_path = "#{source_dir}/#{posts_dir}"
  puts "Listing drafts in #{posts_path}..."

  drafts = Array.new()
  Dir.glob("#{posts_path}/*.*").each_with_index do |post, idx|
    yaml = Preamble.load(post)
    published = yaml[0]["published"]
    if published == false
      post_shortname = post.gsub(/#{posts_path}\//, '')
      drafts.push(post_shortname)
    end
  end

  if drafts.length == 0
    puts "### There are no drafts at present."
    exit 0
  end

  post_options = Array.new(drafts.length)
  drafts.each_with_index do |draft_post, idx|
    post_options[idx] = "#{idx}"
    puts "  [#{idx}]  #{draft_post}"
  end

  publish_index = ask("Which post would you like to publish", post_options)

  post_shortname = drafts[publish_index.to_i]
  post_path = "#{posts_path}/#{post_shortname}"
  yaml = Preamble.load(post_path);
  puts "  Post details:"
  puts "    Title:\t#{yaml[0]["title"]}"
  puts "    Date:\t#{yaml[0]["date"]}"
  puts
  publish_option = ask("Publish with current date (p), existing date (e) or cancel (c)", ['p', 'e', 'c'])

  if publish_option == 'c'
    exit 0
  elsif publish_option == 'p'
    puts "Publishing with current date"
    yaml[0]["published"] = true
    yaml[0]["date"] = Time.now.strftime('%Y-%m-%d %H:%M')

    matchData = post_shortname.match(/^\d{4}-\d{1,2}-\d{1,2}-(.*)$/)
    title_from_filename = matchData[1];

    new_post_path = "#{posts_path}/#{Time.now.strftime('%Y-%m-%d')}-#{title_from_filename}"
    File::delete(post_path)

    open(new_post_path, 'w') do |write_post|
      write_post.puts yaml[0].to_yaml
      write_post.puts "---"
      write_post.puts yaml[1]
    end

    puts "The post has been published as #{new_post_path}"

  elsif publish_option == 'e'
    puts "Publishing with existing date"
    yaml[0]["published"] = true
    open(post_path, 'w') do |write_post|
      write_post.puts yaml[0].to_yaml
      write_post.puts "---"
      write_post.puts yaml[1]
    end
  end
end
{% endcodeblock %}
