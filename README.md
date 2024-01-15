# ROR Ecommerce

## Getting Started

Install RVM with Ruby 2.4.
If you have 2.4 on your system you're good to go.
Please refer to the [RVM](http://beginrescueend.com/rvm/basics/) site for more details.

Copy the `database.yml` for your setup.
For SQLite3, `cp config/database.yml.sqlite3 config/database.yml`.
For MySQL, `cp config/database.yml.mysql config/database.yml` and update your username/password.

If you are using the mysql dmg file to install mysql you will need to edit your ~/.bash_profile and include this:

  export DYLD_LIBRARY_PATH=/usr/local/mysql/lib:$DYLD_LIBRARY_PATH

Install gems and build the app

    gem install bundler
    bundle install
    rake secret # copy/paste the output as `encryption_key` in `config/settings.yml`
    rake db:create:all
    rake db:migrate db:seed
    RAILS_ENV=test rake db:test:prepare
    RAILS_ENV=test rake db:seed

Once everything is set up, start the server with `rails server` and direct your web browser to [localhost:3000/admin/overviews](http://localhost:3000/admin/overviews).
Write down the username/password (these are only shown once) and follow the directions.

## Environmental Variables
    FOG_DIRECTORY     => your bucket on AWS
    AWS_ACCESS_KEY_ID => your access key on AWS
    AWS_SECRET_ACCESS_KEY => your secret key on AWS
    AUTHNET_LOGIN     => if you use authorize.net otherwise change config/settings.yml && config/environments/*.rb
    AUTHNET_PASSWORD  => if you use authorize.net otherwise change config/settings.yml && config/environments/*.rb

## ImageMagick and rMagick on OS X 10.8
------------------------------------

If installing rMagick on OS X 10.8 and using Homebrew to install ImageMagick, you will need to symlink across some files or rMagick will not be able to build.

Do the following in the case of a Homebrew installed ImageMagick(and homebrew had issues):

    * cd /usr/local/Cellar/imagemagick/6.8.9-8/lib
    * ln -s libMagick++-6.Q16.5.dylib   libMagick++.dylib
    * ln -s libMagickCore-6.Q16.2.dylib libMagickCore.dylib
    * ln -s libMagickWand-6.Q16.2.dylib libMagickWand.dylib

    * you may need to change the version path if the imagemagick has been updated

#### Payment Gateways

First, create `config/settings.yml` and change the encryption key and paypal/auth.net information.
You can also change `config/settings.yml.example` to `config/settings.yml` until you get your real info.

To change from authlogic to any other gateway look at the documentation [HERE](http://drhenner.github.com/ror_ecommerce/config.html)

## Paperclip

Paperclip will throw errors if not configured correctly.
You will need to find out where Imagemagick is installed.
Type: `which identify` in the terminal and set

```ruby
Paperclip.options[:command_path]
```

equal to that path in `config/initializers/paperclip.rb`.

Example:

Change:

```ruby
Paperclip.options[:command_path] = "/usr/local/bin"
```

Into:

```ruby
Paperclip.options[:command_path] = "/usr/bin"
```
