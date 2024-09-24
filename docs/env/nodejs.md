```
env http_proxy =http://10.7.105.30:7890
env https_proxy=http://10.7.105.30:7890

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

NVM_NODEJS_ORG_MIRROR=https://npmmirror.com/mirrors/node/ nvm install --lts

node -v

npm -v

npm i docsify-cli -g

docsify -v
```

