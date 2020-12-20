# Recursive Git status
## Quick and dirty Ruby script to recursively check Git status of folders (and folders within folders etc.)

```ruby
#!/usr/bin/env ruby

require 'colorize'

start_dir = ARGV[0]

def recursive_check(directory)
  if File.directory?(File.join(directory, '.git'))
    Dir.chdir(directory)
    puts "Status of #{Dir.getwd}:".colorize(:green)
    puts `git status`
    puts
  end

  subdirectories = Dir.entries(directory).select { |file| File.directory?(File.join(directory, file)) and file != '.' and file != '..' }

  subdirectories.each do |subdirectory|
    recursive_check(File.join(directory, subdirectory))
  end
end

recursive_check(start_dir)
```
