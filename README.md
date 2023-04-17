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
TODO

## Additional Standard Package
1. [Node Js](https://nodejs.org/en)
2. Node Package Manage (npm) (comes with the [Node Js](https://nodejs.org/en) Installation)

References for installation in debian guest can be read [here](https://github.com/nodesource/distributions#debinstall)

In short, in order to install Node (As of this, this installation is using Node Js v19.x) in debian, you can use
(make sure you are on root)
```
curl -fsSL https://deb.nodesource.com/setup_19.x | bash - &&\
apt-get install -y nodejs
```
3. (Optionally) yarn
Make sure [Node Js](https://nodejs.org/en) and npm has been installed
```
npm install --global yarn
yarn --version
```