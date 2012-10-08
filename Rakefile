require 'rubygems'
require 'zip/zip'


desc "Tabkit build script"
task :build , :version do |t, args|

  version = args[:version]
  version ||= Time.now.strftime("%F") # incase someone forgot to put in version or lazy, put in today's day

  # ["content/bindings.xml"]
  everything = Dir.glob "**/*"

  excluded_regexp = /(\.(xpi|zip)|Rakefile)$/i
  included = everything.select do |path|
    path !~ excluded_regexp
  end

  input_filenames = included
  no_of_files = input_filenames.size

  path = "product"
  # Create Dir if not exist
  Dir.mkdir(path) unless File.exists?(path)

  zipfile_name = "tabkit2 #{version}.xpi"
  puts "About to build #{zipfile_name} with #{no_of_files} files"

  Zip::ZipFile.open(File.join(path, zipfile_name), Zip::ZipFile::CREATE) do |zipfile|
    input_filenames.each do |filename|
      # Two arguments:
      # - The name of the file as it will appear in the archive
      # - The original file, including the path to find it
      zipfile.add(filename, filename)
    end
  end

  puts "#{zipfile_name} Built"
end

task default: :build

