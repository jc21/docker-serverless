# docker-serverless

Run serverless commands without having to install nodejs

## Usage

```bash
alias serverless="touch ~/.serverlessrc;docker run --rm -ti -v \"$HOME/.serverless:/root/.serverless\" -v \"$(pwd):/opt/app\" jc21/serverless serverless"

serverless login
```
