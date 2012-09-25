## js.strea.ms

A simple JavaScript Activity Streams implementation.

Example:

``` javascript
var as = 
  AS.activity()
    .actor(AS.person().displayName("James"))
    .verb("post")
    .object(AS.note().content("test"))
    .links(AS.links().alternate([AS.link().href("http://example.org")]).set("canonical",[]))
    .get();

print(as.write());
```

More details to be added later...


## activitystreams.rb

A simple Ruby Activity Streams implementation

Example:
require 'activitystreams'
include ActivityStreams
 
``` ruby
#!/Users/james/.rvm/rubies/ruby-1.9.3-p194/bin/ruby
$: << '.' if !$:.include? '.'
##############################################
# Author: James M Snell (jasnell@gmail.com)  #
# License: Apache v2.0                       #
##############################################
require 'activitystreams'
require 'optparse'

options = {}
optparse = OptionParser.new do|opts|
 opts.banner = "Usage: note [options] content"
 options[:name] = nil
 opts.on( '-n', '--name NAME', 'The name' ) do |x|
   options[:name] = x
 end
 opts.on( '-h', '--help', 'Display this screen' ) do
   puts opts
   exit
 end
end
optparse.parse!

include ActivityStreams
 
STDOUT << activity {
  pretty
  verb :post
  actor person {
    display_name options[:name]
  }
  obj note {
    content ARGV.shift
  }
}
```