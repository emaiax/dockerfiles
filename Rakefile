require "rake"

task :build do
  changed_files.each do |dockerfile|
    image, tag = dockerfile.gsub(/\/Dockerfile/, "").split("/")
    context    = File.dirname(dockerfile)
    tag        ||= "latest"

    exec %{docker build -t emaiax/#{image}:#{tag} #{context}}
    exec %{docker login -u #{ENV["DOCKER_USER"]} -p #{ENV["DOCKER_PASSWORD"]}}
    exec %{docker push emaiax/#{image}:#{tag}}
  end
end

task default: :build

private

def run(cmd)
  puts "[Running] #{cmd}"
  %x{#{cmd}} unless ENV["DEBUG"]
end

def exec(cmd)
  puts "[Running] #{cmd}"
  system cmd unless ENV["DEBUG"]
end

def changed_files
  head, upstream = git_diffs

  if head == upstream
    files = run %{git diff HEAD~ --name-only --diff-filter=d -- '*Dockerfile'}
  else
    files = run %{git diff "#{upstream.chomp}...#{head.chomp}" --name-only --diff-filter=d -- '*Dockerfile'}
  end

  files.split("\n")
end

def git_diffs
  repo   = "https://github.com/emaiax/dockerfiles.git"
  branch = "master"

  head = run %{git rev-parse --verify HEAD}

  run %{git fetch -q #{repo} refs/heads/#{branch}}

  upstream = run %{git rev-parse --verify FETCH_HEAD}

  [head, upstream]
end
