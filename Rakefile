require "rake"

task :build do
  dockerfiles = changed_files

  if dockerfiles.none?
    puts
    puts "No Dockerfiles changed to build."

    exit(0)
  end

  dockerfiles.each do |dockerfile|
    image, tag = dockerfile.gsub(/\/Dockerfile/, "").split("/")
    context    = File.dirname(dockerfile)
    tag        ||= "latest"

    puts
    puts "Building #{image}:#{tag}..."
    puts

    if ENV.fetch("DEBUG", "").empty?
      run %{docker build -t emaiax/#{image}:#{tag} #{context}}

      unless ENV.fetch("DEPLOY_TO_DOCKER_HUB", "").empty?
        run %{docker login -u #{ENV["DOCKER_USER"]} -p #{ENV["DOCKER_PASSWORD"]}}
        run %{docker push emaiax/#{image}:#{tag}}
      end
    end
  end
end

task default: :build

private

def run(cmd)
  puts "[Running] #{cmd}"
  %x{#{cmd}}
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
