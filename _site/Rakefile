def templates
  Dir['*.haml']
end

def file_tasks 
  templates.map do |template|
    { template.split('.haml').first => template }
  end
end

def out_files
  file_tasks.map(&:keys).flatten
end

for file_task in file_tasks 
  file file_task do
    out, template = file_task.each_pair.first
    system "haml #{template} #{out}" 
  end
end

task default: out_files 
