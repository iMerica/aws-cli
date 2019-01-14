# AWS CLI

Fork of Mesosphere's AWS CLI in Docker with various improvements.

## Build

```
docker build -t imichael/aws-cli .
```

Automated build on Docker Hub

[![DockerHub Badge](http://dockeri.co/image/imichael/aws-cli)](https://hub.docker.com/r/mesosphere/aws-cli/)

## Usage

Configure:

```
export AWS_ACCESS_KEY_ID="<id>"
export AWS_SECRET_ACCESS_KEY="<key>"
export AWS_DEFAULT_REGION="<region>"
```

Upload file to S3:

```
./aws.sh s3 cp ../dcos-centos-virtualbox-0.2.1.box s3://downloads.dcos.io/dcos-vagrant/
```

Caveat: Because `aws.sh` mounts the current directory as `/project`, paths to local files must be relative to the current directory.

## Install

To use `aws.sh` as a drop-in replacement for calls to the aws-cli, use one of the following methods:

Add an alias to your shell:

```
alias aws='docker run --rm -t $(tty &>/dev/null && echo "-i") -e "AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}" -e "AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}" -e "AWS_DEFAULT_REGION=${AWS_DEFAULT_REGION}" -v "$(pwd):/project" mesosphere/aws-cli'
```

Or drop it into your path named `aws`:

```
curl -o /usr/local/bin/aws https://raw.githubusercontent.com/mesosphere/aws-cli/master/aws.sh && chmod a+x /usr/local/bin/aws
```

## Maintenance 

- The Docker image build & publish is automated by DockerHub for master commits and tags.
- The awscli and s3cmd packages have handcoded versions in the Dockerfile that need to be bumped manually.

## References

AWS CLI Docs: https://aws.amazon.com/documentation/cli/

