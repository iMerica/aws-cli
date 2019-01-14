# AWS CLI

[![DockerHub Badge](http://dockeri.co/image/imichael/aws-cli)](https://hub.docker.com/r/imichaewl/aws-cli/)

Fork of Mesosphere's AWS CLI in Docker with various improvements.

## Install

Pull the latest image:

    docker pull imichael/aws-cli 


Create AWS Configuration files with neccessary values.

- `~/.aws/credentials`
- `~/.aws/config`

Alias command

    alias aws='docker run --rm -t $(tty &>/dev/null && echo "-i") -e "AWS_DEFAULT_REGION=us-east-2" -v "$(pwd):/project"  -v "${HOME}/.aws:/root/.aws"  imichael/aws-cli'

## Example Usage
Upload file to S3:

```
aws s3 cp ../dcos-centos-virtualbox-0.2.1.box s3://downloads.dcos.io/dcos-vagrant/
```

Caveat: Because `aws-cli` mounts the current directory as `/project`, paths to local files must be relative to the current directory.

## Maintenance 

- The Docker image build & publish is automated by DockerHub for master commits and tags.
- The awscli and s3cmd packages have handcoded versions in the Dockerfile that need to be bumped manually.

## References

AWS CLI Docs: https://aws.amazon.com/documentation/cli/

