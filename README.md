```sh
> export GITHUB_USERNAME=ArinaUrnysheva
 ~                                                                             
> export GITHUB_EMAIL=arinaurnysheva@yandex.ru
 ~                                                                             
> export GITHUB_TOKEN=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
 ~                                                                             
> alias edit=xed   
 ~                                                                             
> cd ${GITHUB_USERNAME}/workspace
                                                 
> source scripts/activate
                                               
> mkdir ~/.config
                                                  
> cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: ssh
EOF
                                                     
> git config --global hub.protocol https
                                                   
> mkdir projects/lab02 && cd projects/lab02
                                                   
> git init
подсказка: Using 'master' as the name for the initial branch. This default branch name
подсказка: is subject to change. To configure the initial branch name to use in all
подсказка: of your new repositories, which will suppress this warning, call:
подсказка: 
подсказка: 	git config --global init.defaultBranch <name>
подсказка: 
подсказка: Names commonly chosen instead of 'master' are 'main', 'trunk' and
подсказка: 'development'. The just-created branch can be renamed via this command:
подсказка: 
подсказка: 	git branch -m <name>
Инициализирован пустой репозиторий Git в /home/arina/ArinaUrnysheva/workspace/.git/
                                    
> git config --global user.name ${GITHUB_USERNAME}
                                      
> git config --global user.email ${GITHUB_EMAIL}
                                     
> git config -e --global

> git remote add origin https://github.com/$\{GITHUB_USERNAME\}/lab02.git

> 
```



















