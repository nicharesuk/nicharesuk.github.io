How I got this website working

I had an issue with 

`gem install jekyll`

Some dependent package `ffi` was failing to build

After much searching I found that adding this:

`LDFLAGS="-L/usr/local/opt/libffi/lib" PKG_CONFIG_PATH="/usr/local/opt/libffi/lib/pkgconfig" gem install bundler jekyll`

Allowed jekyll to install correctly

(Lots of people online were saying you could just reinstall xcode commandline but that didn't work for me)

(People also recommended installing the header packages for Mac OS 10.14 but that also didn't solve this problem)

After all of this then when I tried to install the so-simple theme I had a problem with `nokogiri`

Luckily I found a fix online:

`bundle config build.nokogiri --use-system-libraries --use-system-libraries=true --with-xml2-include="$(xcrun --show-sdk-path)"/usr/include/libxml2`

This sets it so that when bundler tries to build nokogiri it will also include these arguments that it needs

So I was now safe to run Bundle Update/Install when I needed to, and luckily ffi was cached so I didn't have to use the first code example each time

Another issue with the So-Simple theme is that when you run just using normal jekyll everything is fine but when you use Github pages versions of jekyll it ignores the theme's folders that start with a "_"

So this didn't include the navigation.yml file in the _data directory. So you have to manually go add those in.

I also had the issue where the example template created by running `jekyll new .` had an invalid date format that broke the build, so I excluded the vendor `  - vendor/bundle/`

MORE ISSUES:

I had another issue where my site was still showing 404 even though it successfully built. The issue seemed to be because I forked the So-Simple repo, so to solve this I just recreated my repo and reuploaded it, not forking it this time. My guess from reading online made it seem that becuase there was a gh-pages branch that it was trying to pull from that or something.