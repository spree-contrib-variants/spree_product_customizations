SpreeProductCustomizations
==========================

This Spree extension allows adding custom calculations to products that affect the pricing. E.g. you could sell fabric by the metre with a custom multiplier.

This is a newer version of 1/2 of the functionality of spree_flexi_variants. It includes the product customizations without the ad-hoc options.

It seems to be working now, if you see any bugs please open an issue or send a pull request.

Master will be the most up to date branch. As we update master for newer versions of Spree we'll create a branch for the previous supported version.

Installation
------------

Add spree_product_customizations to your Gemfile:

```ruby
gem "spree_product_customizations", github: "spree-contrib-variants/spree_product_customizations", branch: "master"
```

Bundle your dependencies and run the installation generator:

```shell
bundle
bundle exec rails g spree_product_customizations:install
```

Custom Calculators
------------------

You can add your own calculators to your app without having to fork this repo. 

First create your calculator files and put them in the right folders like so. Look in the same folders in this repo for the built in calculators; copy and modify the one that's closest to what you need.

```
app/models/spree/calculator/curtain_area.rb
app/views/spree/products/customizations/calculator/_curtain_area.html.erb
app/views/spree/products/customizations/calculator_type/_curtain_area.html.erb
```

Then register the calculator(s) in your `config/application.rb`:

```ruby
module MyWebsite
  class Application < Rails::Application
    ...

    initializer "MyWebsite.register.calculators" do |app|
      app.config.spree.calculators.product_customization_types.push(
        Spree::Calculator::CurtainArea
      )
    end
  end
end
```

Testing
-------

First bundle your dependencies, then run `rake`. `rake` will default to building the dummy app if it does not exist, then it will run specs. The dummy app can be regenerated by using `rake test_app`.

```shell
bundle
bundle exec rake
```

When testing your applications integration with this extension you may use it's factories.
Simply add this require statement to your spec_helper:

```ruby
require 'spree_product_customizations/factories'
```

Copyright (c) 2014 [name of extension creator], released under the New BSD License
