# Docusaurus-ova
A repository for configuring Docusaurus in a Debian guest (VirtualBox)

## Debian Guest OVA File
The OVA standard file for the debian guest with docusaurus can be downloaded from
[https://is3.cloudhost.id/francis/sp231/ova-docusaurus-standarized-v.1.0.0.ova](https://is3.cloudhost.id/francis/sp231/ova-docusaurus-standarized-v.1.0.0.ova)

> Attention: The OVA is quite large, and my cloud provider is cheap, so maybe try to use multi-connection downloads such as using `aria2c` or Free Download Manager.
## How to use the OVA
1. Login using 
```
username: cbkadal
password: cbkadal
```
2. change the directory to code/os-documentation
```
cd code/os-documentation
```
3. Run the necessary preperation commands
```
yarn build
yarn serve
```

## Other OVA notes
| Internal port | External Port |
|---|---|
|22|6022|
|3000|5001|
|4000|5000|

## How to setup Github repository
1. Log in to your Github account
2. Click the new repository button
![new repository](/img/new-repository.png)
3. Fill in the repository name and optionally the description section
![repo name](/img/name-desc.png)
4. Optionally you could add a license from github
![license](/img/license.png)
5. Finally once everything is set, you can now create the repository
![create](/img/create.png)

## How to setup the debian guest with Docusaurus
A script is included in the OVA called `prepare-nodejs.sh`. Running it should be sufficient to setup everything we need to setup all NodeJS and other system packages needed.

```bash
export DEBS1="apt-file aptitude autoconf automake bc bison build-essential cowsay curl dateutils dos2unix fail2ban flex gawk gettext git git-flow gnupg gnupg-agent libacl1-dev libcap-dev libelf-dev liblocale-msgfmt-perl libncurses-dev libseccomp-dev libselinux1-dev libssl-dev locales-all manpages-dev net-tools parted python-is-python3 rsync sysstat sysvbanner texinfo unzip vim x11-apps"
export DEBS2="acct bsdmainutils clang-format expect faketime finger fuse kmod libc6-dev libfuse-dev lynx pkg-config sudo tmux util-linux"
echo "Updating system and installing utilities..." && \
time su -c "apt update && apt upgrade -y && apt install -y $DEBS1 && apt install -y $DEBS2 && apt install -y coreutils" && \
echo "Done updating system and installing utilities" && \
echo "Downloading NVM script" && \
time curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash && \
export NVM_DIR="$HOME/.nvm" && \
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" && \
echo "Done downloading and installing NVM" && \
echo "Installing LTS Node JS" && \
time nvm install --lts && \
echo "Done installing LTS Node JS" && \
echo "Installing NPM and Yarn" && \
time su -c "apt install -y npm" && \
time npm install --global yarn && \
echo "Done. Environment ready."
```

### Explaination

#### Node JS
Docusaurus is built on top of React, a JavaScript framework used to build user interfaces. 
To be able to "build" Docusaurus websites, we first need to setup NodeJS.
Normally, this can be done thru package managers (like `apt`). However, the version of NodeJS available through `apt` is no longer maintained. Therefore, we can either install it manually through [the official website](https://nodejs.org/en/download), or we can use a script that helps us with that, such as [node version manager](https://github.com/nvm-sh/nvm#install--update-script).

Using `nvm`, all we need to do is run the two scripts given in their repository (linked above), and we'd have access to `nvm`. Then, we just need to run `nvm install --lts`. If no longer needed, we can run `nvm uninstall --lts`.

Otherwise, we can download the source directly by:
```
curl -fsSL https://deb.nodesource.com/setup_19.x | bash - &&\
apt-get install -y nodejs
```

>Note: This guest uses `nvm` to install `Node.js`
#### Package Managers
To manage JavaScript packages used by Docusaurus, you can use either npm (which comes bundled with Node.js) or Yarn. In this guide, we'll use Yarn. 

To install Yarn, run the following script
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - &&\
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list &&\
sudo apt-get update && sudo apt-get install yarn
```
or, alternatively
```
npm install -g yarn
```
> Note: the `yarn` package available from `apt` is not the package we want!
> `yarn` is installed from `npm` in this debian guest.
### Running a local preview
First, we'll install the packages required by docusaurus.
```
yarn install
```
To have a local preview that live-updates, run
```
yarn start
```

### Optimized Deployment Build
To get an optimized deployment build, run
```
yarn build
```
To get a preview of this build, run
```
yarn serve
```

### Deployment
Deployment instructions to Github Pages or other platforms can be found [here](https://docusaurus.io/docs/deployment)