# GPG Key

#### Secret key sample

> D5D1D296E920B6FA

#### 1.Generate new gpg key

> gpg --full-gen-key

#### 2.Get list of existence gpg key

> gpg --list-secret-keys --keyid-format LONG 

#### 3.Export gpg public key of that ID

> gpg --armor --export gpg secret key

#### 4.Set gpg secret key global on git

> git config --global gpg.program "c/gnupg/bin/gpg.exe"
> git config --global user.s igningkey D5D1D296E920B6FA

#### Share your public key

> gpg --send-keys gpg secret key

#### Optional: try disable TTY if you have problems with making auto-signed commits from your IDE or other software
> echo 'no-tty' >> /c/Users/LinhNguyen/.gnupg/gpg.conf

#### Export gpg key

> gpg --export-secret-keys YOUR_ID_HERE > private.key

#### Import gpg key on another machine

> gpg --import private.key