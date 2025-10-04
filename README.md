# setup-dual-git-in-win

Steps to setup multiple git account in one system

Step 1- 
> cd ~/.ssh/
> ssh-keygen -t ed25519 -C "git@workmail.com"
> ssh-keygen -t ed25519 -C "git@personalmail.com"

> eval "$(ssh-agent -s)"

> ssh-add id_work
> ssh-add id_personal

> cat id_work.pub -> paste output to -> work github accout setting ssh 

> cat id_personal.pub -> paste output to -> personal github accout setting ssh 

> nano config
  # Work Github
	Host github-work
			hostname github.com
			User git
			IdentifyFile ~/.ssh/id_work

	# Personal Github
	Host github-personal
			hostname github.com
			User git
			IdentifyFile ~/.ssh/id_personal
			
> ssh -T git@github-personal

> git clone git@github-personal:mdsaif45/repo.git
> git clone git@github-work:company/repo.git

cd D://personal-repos/my-repo
git config user.name "MD SAIF"
git config user.email "mdsaif0405@gmail.com"
