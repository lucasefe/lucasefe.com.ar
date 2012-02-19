---
layout: post
title: "Themes for Rails With Assets Pipeline Support"
date: 2012-02-19 18:14
comments: true
categories: 
---

Themes For Rails, version 0.5.0.pre, has been released. It includes a couple of bug fixes, and many improvements. The most important one is the support for the Rails Assets Pipeline. In reality, this is a consequence of an important enhancement. 

## The problem

In the beginning, a Theme was a collection of static files (images, css and js files), and dynamic views (haml, erb, or whatever rails supported). Each theme was one single package, normally organized on the themes folder at the Rails application's root. 

The folder containing each themes should look like this: 

    dark # <--- Theme name
      stylesheets
      javascripts
      images
      views
        layouts

After some time, I realized things doesn't always are used the way I thought they would be. So some people asked me about how to change this layouts of files (I also saw forks on github existing only to change this). 

## The solution

To make this story a little but shorter, now you can change where the assets are stored, and how. 

Let's see an example.

### Hey, I don't want all the static files right there, on the root of theme. 

Ok, you can change it like this.

    # config/initializers/tfr.rb
    ThemesForRails.config do |config|
      config.assets_dir = ":root/themes/:name/assets" 
    end

So your static assets will be on `themes/pink/assets/stylesheets`, `themes/pink/assets/javascripts` and `themes/pink/assets/images`, but your views will still need to be stored on `themes/pink/views` in order to be found. 

### What about Assets Pipeline support?

    ThemesForRails.config do |config|
      # themes_dir is used to allow ThemesForRails to list available themes. 
      # It is not used to resolve any paths or routes.
      config.themes_dir = ":root/app/assets/themes"

      # assets_dir is the path to your theme assets.
      config.assets_dir = ":root/app/assets/themes/:name"

      # views_dir is the path to your theme views
      config.views_dir =  ":root/app/views/themes/:name"

      # themes_routes_dir is the asset pipeline route base. 
      # Because of the way the asset pipeline resolves paths, you do
      # not need to include the 'themes' folder in your route dir.
      #
      # for example, to get application.css for the default theme, 
      # your URL route should be : /assets/default/stylesheets/application.css
      config.themes_routes_dir = "assets"
    end

You can visit the [wiki page](https://github.com/lucasefe/themes_for_rails/wiki/Assets-Pipeline-Integration) on [GitHub](https://github.com/lucasefe/themes_for_rails) for more information. 

## The conclusion

So this is not the final release. We need some testing so if you are using this gem, please, update to the pre version and submit all the bug you can find. I'll do my best to fix them. 

    gem 'themes_for_rails', '0.5.0.pre'

Thanks, and I hope you find this gem usefull. 