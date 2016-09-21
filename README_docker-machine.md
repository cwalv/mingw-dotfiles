# docker-machine mingw tweaks

pull completion files to `/usr/share/bash-completion`

```
completiondir=/usr/share/bash-completion/completions
files=(docker-machine docker-machine-wrapper docker-machine-prompt)
for f in "${files[@]}"; do
  curl -L https://raw.githubusercontent.com/docker/machine/v$(docker-machine --version | tr -ds ',' ' ' | awk 'NR==1{print $(3)}')/contrib/completion/bash/$f.bash > $completiondir/$f
done

curl -L https://raw.githubusercontent.com/docker/compose/$(docker-compose --version | awk 'NR==1{print $NF}')/contrib/completion/bash/docker-compose > $completiondir/docker-compose
curl -L https://github.com/docker/docker/raw/master/contrib/completion/bash/docker > $completiondir/docker
```

update `.bashrc` with aliases:
```
alias dkrm="docker-machine"
_completiondir=/usr/share/bash-completion/completions
source $_completiondir/docker-machine
complete -F _docker_machine docker-machine.exe dkrm
```
