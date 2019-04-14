# vim:ts=2:sw=2:et:
require 'spec/rake/spectask'
require 'csv'
require 'yaml'

Spec::Rake::SpecTask.new do |t|
  t.libs << 'lib'
  t.spec_opts = ["--color" ]
end

desc 'Update rules'
task :update_rules do
  CSV.open(File.dirname(__FILE__) + '/registry.txt', 'r', col_sep: '|') do |csv|
    lines = csv.readlines
    lines.shift
    rules = {}
    lines.each do |line|
      bban_pattern = line[5].gsub(/[()^$]/, '')
      rules[line[0]] = {
        'length' => line[10].to_i,
        'bban_pattern' => bban_pattern
      }
    end

    File.open(File.dirname(__FILE__) + '/lib/iban-tools/rules.yml', 'w') do |file|
      rules_string = rules.to_yaml.gsub("\\\\", "\\")
      rules_string = rules_string.gsub("\"", "'")
      file.write(rules_string)
    end
  end
end
