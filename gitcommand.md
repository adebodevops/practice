"""
# Setting SSH


    #  checking exist keys
    adeboodunsi@Adebos-Macbook-Air learngit % ls -al ~/.ssh   ##To check if i have an active ssh key
    total 16
    drwx------   4 adeboodunsi  staff   128  8 Sep  2022 .
    drwxr-xr-x+ 39 adeboodunsi  staff  1248 25 Mar 14:03 ..
    -rw-------   1 adeboodunsi  staff   751 27 Jan 10:23 known_hosts
    -rw-r--r--   1 adeboodunsi  staff    93  8 Sep  2022 known_hosts.old

    
    # Generate a key
    adeboodunsi@Adebos-Macbook-Air learngit % ssh-keygen -t ed25519 -C "adebodevops@gmail.com"
    Generating public/private ed25519 key pair.
    Enter file in which to save the key (/Users/adeboodunsi/.ssh/id_ed25519): 
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Passphrases do not match.  Try again.
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 


    #  Generated key
    Your identification has been saved in /Users/adeboodunsi/.ssh/id_ed25519
    Your public key has been saved in /Users/adeboodunsi/.ssh/id_ed25519.pub
    The key fingerprint is:
    SHA256:L5xProawcRZ/WpwngGNQT0veKdM+YrCcYqvuy5YXndY adebodevops@gmail.com
    The key's randomart image is:
    +--[ED25519 256]--+
    |     .. o        |
    |    .  = + .     |
    |     ...* +      |
    |     .=+.+       |
    |    oo+*Soo.     |
    |   .+o*oE+*..    |
    |   ..O .++oo     |
    | .o.o . o=       |
    | +*o   ...o      |
    +----[SHA256]-----+


    #  Add key to key-agent
    adeboodunsi@Adebos-Macbook-Air learngit % eval "$(ssh-agent -s)"
    Agent pid 2354

    #  Configure key to ba global (mac requirement)
    adeboodunsi@Adebos-Macbook-Air learngit % cd ..
    
    adeboodunsi@Adebos-Macbook-Air ~ % cd .ssh       
    adeboodunsi@Adebos-Macbook-Air .ssh % ls -a
    .               ..              id_ed25519      id_ed25519.pub  known_hosts     known_hosts.old

    adeboodunsi@Adebos-Macbook-Air ~ % touch ~/.ssh/config
    adeboodunsi@Adebos-Macbook-Air ~ % cd .ssh

    adeboodunsi@Adebos-Macbook-Air .ssh % vim config
    adeboodunsi@Adebos-Macbook-Air ~ % pbcopy < ~/.ssh/id_ed25519.pub
    adeboodunsi@Adebos-Macbook-Air ~ % cd .ssh
    adeboodunsi@Adebos-Macbook-Air .ssh % ls
    config          id_ed25519      id_ed25519.pub  known_hosts     known_hosts.old
    adeboodunsi@Adebos-Macbook-Air .ssh % vim id_ed25519.pub

    # Testing SSH connection to hithub hosting service
    adeboodunsi@Adebos-Macbook-Air ~ % ssh -T git@github.com
    The authenticity of host 'github.com (140.82.121.4)' can't be established.
    ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
    This key is not known by any other names
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes


# Git

    search for git credentials
        1. sudo git config --get user."[email or user]" 
        2. sudo git config --list
    create git credentials
        1. sudo git config --global user.name “[firstname lastname]”
        2. sudo git config --global user.email “[valid-email]”
    edit git credentials
        1. sudo git config --global --edit
        2. sudo git config --global --replace-all user."[email or user]" "[your new email or your new user]"
        3. git commit --amend --reset-author ( reset commit author)
    delete git credentials
        1. sudo git config --global --unset user."[email or user]"
        2. sudo git config --global --unset-all user."[email or user]"

    # Git sometime set of default system credentials as git credentials but one can edit the global  credentials and/or change commiter using (git commit --amend --reset-author)

    # Error sample
    [master 253631a] first commit
    Committer: Adebo Odunsi <adeboodunsi@Adebos-Macbook-Air.local>
    Your name and email address were configured automatically based
    on your username and hostname. Please check that they are accurate.
    You can suppress this message by setting them explicitly:

        git config --global user.name "Your Name"
        git config --global user.email you@example.com

    After doing this, you may fix the identity used for this commit with:
        git commit --amend --reset-author

    # Correction sample
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 practice.txt
    adeboodunsi@Adebos-Macbook-Air learngit % git config --global user.name "Adebo Odunsi"
    adeboodunsi@Adebos-Macbook-Air learngit % git config --global user.email adebodevops@gmail.com

    # pushing to git
    adeboodunsi@Adebos-Macbook-Air learngit % git init
    Reinitialized existing Git repository in /Users/adeboodunsi/learngit/.git/
    adeboodunsi@Adebos-Macbook-Air learngit % git add practices.txt
    adeboodunsi@Adebos-Macbook-Air learngit % git remote add origin https://github.com/adebodevops/practice.git

    adeboodunsi@Adebos-Macbook-Air learngit % touch README.md
    adeboodunsi@Adebos-Macbook-Air learngit % git add README.md
    adeboodunsi@Adebos-Macbook-Air learngit % ls
    README.md       gitcommand.txt  practices.txt
    adeboodunsi@Adebos-Macbook-Air learngit % git branch -M main
    adeboodunsi@Adebos-Macbook-Air learngit % git push -u origin main

#error
    remote: Permission to adebodevops/practice.git denied to adeyy12.
    fatal: unable to access 'https://github.com/adebodevops/practice.git/': The requested URL returned error: 403

    # clue: I was had a little mix up. I was using HTTPS instead of SSH.
#Fix
    adeboodunsi@Adebos-Macbook-Air learngit % git remote rm origin

    adeboodunsi@Adebos-Macbook-Air learngit % git remote -v
    adeboodunsi@Adebos-Macbook-Air learngit % git remote add origin git@github.com:adebodevops/practice.git  


    adeboodunsi@Adebos-Macbook-Air learngit % git push -u origin main
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 226 bytes | 226.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To github.com:adebodevops/practice.git
    * [new branch]      main -> main
    branch 'main' set up to track 'origin/main'.
    adeboodunsi@Adebos-Macbook-Air learngit % """