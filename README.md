# AWS CLI

Fork of Mesosphere's AWS CLI in Docker with various improvements.

## Install

```
docker pull imichael/aws-cli 
```

Automated build on Docker Hub

[![DockerHub Badge](http://dockeri.co/image/imichael/aws-cli)](https://hub.docker.com/r/mesosphere/aws-cli/)

## Usage

Configure:

- `~/.aws/credentials`
- `~/.aws/config`

Upload file to S3:

```
./aws.sh s3 cp ../dcos-centos-virtualbox-0.2.1.box s3://downloads.dcos.io/dcos-vagrant/
```

Caveat: Because `aws.sh` mounts the current directory as `/project`, paths to local files must be relative to the current directory.

## Install

To use `aws.sh` as a drop-in replacement for calls to the aws-cli, use one of the following methods:

Add an alias to your shell:

```
alias aws='docker run --rm -t $(tty &>/dev/null && echo "-i") -e "AWS_DEFAULT_REGION=us-east-2" -v "$(pwd):/project"  -v "${HOME}/.aws:/root/.aws"  imichael/aws-cli'
```

## Maintenance 

- The Docker image build & publish is automated by DockerHub for master commits and tags.
- The awscli and s3cmd packages have handcoded versions in the Dockerfile that need to be bumped manually.

## References

AWS CLI Docs: https://aws.amazon.com/documentation/cli/

