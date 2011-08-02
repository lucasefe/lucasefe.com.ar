---
layout: post
title: "Adding Custom Input Fields to Simple Form"
date: 2010-10-04 17:48
comments: true
categories: 
  - Ruby
---

In a project I am using [Simple Form](http://github.com/plataformatec/simple_form) from the guys of PlataformaTec as a Form Builder. At the beginning of the project, I decided to switch from formtastic to this one because I am big fan of what José Valim is doing. I really like his code, and I think that what he writes is always (as far as I know) extendible, usable, and of course, simple to use. 

So last week I needed to use a particular kind of input field. We needed to show a box like this one:

![subdomain](/images/subdomain.png)
  
Pretty self explanatory, right? 

I wanted to be able to write something like this in my view files (in [HAML](http://haml-lang.com/))

``` ruby
    = simple_form_for :organization do |f|
      # ...
      =f.input :subdomain, :as => :subdomain, :domain => 'foooo.com'
```

So in order to achieve this, we only needed to add this to config/initializers/simple_form_extensions.rb (for example).
  
``` ruby
    module SimpleForm
      module Inputs
        class SubdomainInput < Base
          def input
            "\#{protocol}\#{@builder.text_field(attribute_name, input_html_options)}.\#{domain}"
          end
          def domain
            input_options[:domain]
          end
          def protocol
            input_options[:protocol] || "http://"
          end
        end
      end
    end
```

The key part here is to name the class properly, so when you do :as => :my_class, your MyClass gets called automatically. 

Simple Form is very well structured, and provides lots of ways to customize its functionality. Check the [readme](http://github.com/plataformatec/simple_form/blob/master//README.rdoc) file to see what you can do without having to create a custom input class like SubdomainInput. Also, you can check [this week's railscasts](http://railscasts.com/episodes/234-simple-form). 
