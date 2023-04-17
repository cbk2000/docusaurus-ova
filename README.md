# Docusaurus-ova
A repository for configuring docusaurus in debian guest (virtual box)

## Debian Guest OVA File
The OVA standard file for the debian guest with docusaurus can be downloaded from
[https://is3.cloudhost.id/francis/sp231/appliances/docusaurus.ova](https://is3.cloudhost.id/francis/sp231/appliances/docusaurus.ova)

## How to use the OVA
1. Login to your debian guest
2. change the directory to code/os-documentation
```
cd code/os-documentation
```
3. Run the necessary preperation commands
```
yarn build
yarn serve
```

## How to setup Github repository
1. Login to your Github account
2. Press the new repository button
![new repository](/img/new-repository.png)
3. Fill in the repository name and optionally the description section
![repo name](/img/name-desc.png)
4. Optionally you could add a license from github
![license](/img/license.png)
5. Finally once everything is set, you can now create the repository
![create](/img/create.png)

## How to setup the debian guest with Docusaurus

### Node JS
Docusaurus is built on top of React, a JavaScript framework used to build user interfaces. 
To be able to "build" Docusaurus websites, we first need to setup NodeJS.
Normally, this can be done thru package managers (like `apt`). However, the version of NodeJS available through `apt` is no longer maintained. Therefore, we can either install it manually through [the official website](https://nodejs.org/en/download), or we can use a script that helps us with that, such as [node version manager](https://github.com/nvm-sh/nvm#install--update-script).

Using `nvm`, all we need to do is run the two scripts given in their repository (linked above), and we'd have access to `nvm`. Then, we just need to run `nvm install --lts`. If no longer needed, we can run `nvm uninstall --lts`.

Otherwise, we can download the source directly by:
```
curl -fsSL https://deb.nodesource.com/setup_19.x | bash - &&\
apt-get install -y nodejs
```
### Package Managers
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
Note: the `yarn` package available from `apt` is not the package we want!

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
