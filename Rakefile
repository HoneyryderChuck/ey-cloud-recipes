TOPDIR = File.dirname(__FILE__)

desc "Test your cookbooks for syntax errors"
task :test do
  puts "** Testing your cookbooks for syntax errors"
  Dir[ File.join(TOPDIR, "cookbooks", "**", "*.rb") ].each do |recipe|
    sh %{ruby -c #{recipe}} do |ok, res|
      if ! ok
        raise "Syntax error in #{recipe}"
      end
    end
  end
end

desc "By default, run rake test"
task :default => [ :test ]

desc "Create a new cookbook (with COOKBOOK=name)"
task :new_cookbook do
  create_cookbook(File.join(TOPDIR, "cookbooks"))
end

def create_cookbook(dir)
  raise "Must provide a COOKBOOK=" unless ENV["COOKBOOK"]
  puts "** Creating cookbook #{ENV["COOKBOOK"]}"
  sh "mkdir #{File.join(dir, ENV["COOKBOOK"], "attributes").gsub(/[\/]/,'\\') }" 
  sh "mkdir #{File.join(dir, ENV["COOKBOOK"], "recipes").gsub(/[\/]/,'\\')}" 
  sh "mkdir #{File.join(dir, ENV["COOKBOOK"], "definitions").gsub(/[\/]/,'\\')}" 
  sh "mkdir #{File.join(dir, ENV["COOKBOOK"], "libraries").gsub(/[\/]/,'\\')}" 
  sh "mkdir #{File.join(dir, ENV["COOKBOOK"], "files", "default").gsub(/[\/]/,'\\')}" 
  sh "mkdir #{File.join(dir, ENV["COOKBOOK"], "templates", "default").gsub(/[\/]/,'\\')}" 
  unless File.exists?(File.join(dir, ENV["COOKBOOK"], "recipes", "default.rb"))
    open(File.join(dir, ENV["COOKBOOK"], "recipes", "default.rb"), "w") do |file|
      file.puts <<-EOH
#
# Cookbook Name:: #{ENV["COOKBOOK"]}
# Recipe:: default
#
EOH
    end
  end
end
