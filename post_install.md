## These are my setup steps upon creating a new virtual machine
Written Summer (June 26th, 2018)
### The iso Bionic Beaver Ubuntu 18.04
here's where you grab the iso
[Download Ubuntu 18.04](http://releases.ubuntu.com/18.04/ubuntu-18.04-desktop-amd64.iso)

### Virtualbox
#### Mac OSX
[Download virtualbox for Mac OSX](https://download.virtualbox.org/virtualbox/5.2.12/VirtualBox-5.2.12-122591-OSX.dmg)
#### Windows 10
[Download virtualbox for Windows 10](https://download.virtualbox.org/virtualbox/5.2.12/VirtualBox-5.2.12-122591-Win.exe)
Follow instructions 
#### Extensions download ALL PLATFORMS
[Download the virtualbox extensions](https://download.virtualbox.org/virtualbox/5.2.12/Oracle_VM_VirtualBox_Extension_Pack-5.2.12.vbox-extpack)

### After installation via virtualbox
The usual...
```bash
sudo apt update
sudo apt upgrade
```
the extras
```bash
sudo apt install ubuntu-restricted-extras
sudo apt install libdvd-pkg
```
add repositories
```bash
sudo add-apt-repository ppa:otto-kesselgulasch/gimp
sudo add-apt-repository -y ppa:gnome3-team/gnome3
sudo add-apt-repository -y ppa:webupd8team/java
sudo add-apt-repository -y ppa:transmissionbt/ppa
```

Manually went to "software & update". In the other software tab, enabled “Canonical Partners”

update after adding the new repositories
```bash
sudo apt update
```
Get and config git
```bash
sudo apt -y install git
git config --global user.name "yournamehere"
git config --global user.email "youremail@here.com"
```
confirm
```bash
cat ~/.gitconfig
```
install some extras
```bash
sudo apt install vlc gimp gimp-data gimp-plugin-registry gimp-data-extras bleachbit openjdk-8-jre oracle-java8-installer unace unrar zip unzip p7zip-full p7zip-rar sharutils rar uudeview mpack arj cabextract file-roller mencoder flac faac faad sox ffmpeg2theora libmpeg2-4 uudeview mpeg3-utils mpegdemux liba52-dev mpeg2dec vorbis-tools id3v2 mpg321 mpg123 icedax lame libmad0 libjpeg-progs libdvdcss2 libdvdread4 libdvdnav4 ubuntu-restricted-extras ubuntu-wallpapers*
```
Note: last time I did this I had to uninstall synaptic...got errors with gtk+

Update again...might be superfluous here
```bash
sudo apt update
```
Time to get the latest **stable** node via node version manager 
```bash
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```
To update your shell environment with new NVM settings either close and re-open your terminal session or enter:
```bash
source ~/.profile
```
list all the latest versions
```bash
nvm ls-remote
```
Note - I made the mistake of installing 10.4.1, and wound up having many unexpected errors when setting up different stacks.  Spent more time trouble shooting than was worth it.
install node
```bash
nvm install 8.11.3
```
install express globally
```bash
npm install -g express
```

You can confirm what is globally installed by entering:
```bash
npm ls -gp --depth=0
```
Messing around with express
```bash
npm install sails -g
sails new test-project
cd test-project
sails lift
```
generate a gpg key
```bash
gpg --full-gen-key
```

Install the Postgres package along with a -contrib package that adds some additional utilities and functionality:
```bash
sudo apt install postgresql postgresql-contrib
sudo apt install postgresql-client
```
The PostgreSQL server will start after reboot. To manipulate this default behavior you can either disable or enable the PostreSQL start after reboot by:
shut it down
```bash
sudo systemctl disable postgresql
```
or start it up
```bash
sudo systemctl enable postgresql
```
By default the PostgreSQL server will listen only on a local loop-back interface 127.0.0.1. If you need to configure your PostreSQL server to listen on all networks you will need to configure its main configuration file /etc/postgresql/10/main/postgresql.conf:
edit the conf file
```bash
sudo nano /etc/postgresql/10/main/postgresql.conf
```
and add the following line somewhere to the CONNECTIONS AND AUTHENTICATION section:
```bash
listen_addresses = '*'
```
Once the configuration is completed restart PostreSQL server:
```bash
sudo service postgresql restart
```
The PostreSQL server should be now listening on socket 0.0.0.0:5432. You can confirm this by executing the ss command:
```bash
ss -nlt
```
you should see...
State Recv-Q Send-Q Local Address:Port Peer Address:Port
LISTEN 0 128 0.0.0.0:22 0.0.0.0:*
LISTEN 0 5 127.0.0.1:631 0.0.0.0:*
LISTEN 0 128 0.0.0.0:5432 0.0.0.0:*
LISTEN 0 128 [::]:22 [::]:*
LISTEN 0 5 [::1]:631 [::]:*

Next, to accept connections from a remote PostreSQL client to all databases and all users 
add the following line to /etc/postgresql/10/main/pg_hba.conf
```bash
host all all 0.0.0.0/0 trust
```
# Install pip and pipenv
```bash
sudo apt install python3-pip python3-dev
pip3 install --user pipenv
```
Notes & How Tos

## Setting up python, pipenv and jupyter notebook on Ubuntu 18.04
05 May 2018
[https://matthewbrown.io/2018/05/05/setting-up-my-python-workspace-2018/
](https://matthewbrown.io/2018/05/05/setting-up-my-python-workspace-2018/)

# Add pipenv (and other python scripts) to PATH
```bash
echo "PATH=$HOME/.local/bin:$PATH" >> ~/.bashrc
source ~/.bashrc
```
Create a new project and install some dependencies (include jupyter)
```bash
mkdir project-name && cd project-name
pipenv install numpy matplotlib jupyter
pipenv shell
pipenv run jupyter notebook
```
### Node package stuff
This removes all globally installed node packages
```bash
npm ls -gp --depth=0 | awk -F/ '/node_modules/ && !/\/npm$/ {print $NF}' | xargs npm -g rm
```

## Setting up PEVN

```bash
npm install express-generator -g
express pevn-starter
```
you'll see the following...
warning: the default view engine will not be jade in future releases
warning: use `--view=jade' or `--help' for additional options

create : pevn-starter/
create : pevn-starter/public/
create : pevn-starter/public/javascripts/
create : pevn-starter/public/images/
create : pevn-starter/public/stylesheets/
create : pevn-starter/public/stylesheets/style.css
create : pevn-starter/routes/
create : pevn-starter/routes/index.js
create : pevn-starter/routes/users.js
create : pevn-starter/views/
create : pevn-starter/views/error.jade
create : pevn-starter/views/index.jade
create : pevn-starter/views/layout.jade
create : pevn-starter/app.js
create : pevn-starter/package.json
create : pevn-starter/bin/
create : pevn-starter/bin/www

change directory:
```bash
cd pevn-starter
```
install dependencies:
bash```
npm install
```
run the app:
```bash
DEBUG=pevn-starter:* npm start
```
you'll get ...

ERROR MSG:
 npm WARN deprecated jade@1.11.0: Jade has been renamed to pug, please install the latest version of pug instead of jade
 npm WARN deprecated constantinople@3.0.2: Please update to at least constantinople 3.1.1
 npm WARN deprecated transformers@2.1.0: Deprecated, use jstransformer

*** FROM: https://stackoverflow.com/questions/38667142/node-js-noobie-trying-to-follow-a-tutorial-need-to-change-jade-reference-to-pu
*** If you want to change jade to pug you can run the following from the command line:
*** npm uninstall jade --save
*** then
*** npm install pug --save
*** in order to remove modules that are not in your package.json file use the prune command:
*** npm prune
```bash
npm uninstall jade --save
npm install pug --save
npm prune

npm uninstall constantinople@3.0.2 --save
npm install constantinople@3.1.1 --save
npm prune

npm uninstall transformers --save
npm install jstransformer --save
npm prune
```
Then I name all my files with the .pug extension like layout.pug. In my Express app, I use the Pug templating engine:

```pug
// view engine setup
app.set('view engine', 'pug');
app.set('views', __dirname + '/views');
```
So for this example, given we have views/index.jade(***pug now) we will want to place it’s associated VueJS app and styles in client/css/index.css, client/js/index.js and /client/js/Index.vue such that when that Jade view is rendered, it will run the Index Vue app.

added index.js and Index.vue using code provided in example

Webpack

In order to create a packaged index.js asset file for our view, we will need to install Webpack, VueJS and its associated dependencies:
```bash
npm install webpack extract-text-webpack-plugin assets-webpack-plugin babel-core babel-loader babel-preset-es2015 css-loader file-loader style-loader url-loader vue-template-compiler --save-dev
npm install vue express-webpack-assets webpack-dev-middleware webpack-hot-middleware
```
PostgreSQL

Lastly let’s go ahead and add pg support by installing sequelize ORM and associated dependencies:
```bash
npm install sequelize pg pg-hstore --save
npm install sequelize-cli --save-dev
./node_modules/.bin/sequelize init
```
```bash
~/Projects/pevn/pevn-starter$ ./node_modules/.bin/sequelize init
```
Sequelize CLI [Node: 10.4.1, CLI: 4.0.0, ORM: 4.37.10]

Created "config/config.json"
Successfully created models folder at "/home/aleska/Projects/pevn/pevn-starter/models".
Successfully created migrations folder at "/home/aleska/Projects/pevn/pevn-starter/migrations".
Successfully created seeders folder at "/home/aleska/Projects/pevn/pevn-starter/seeders".

Running those commands will create some setup code, you will just need to update your config/config.json with the right connection info:
```json
{
"development": {
"username": "postgres",
"password": "postgres4!,
"database": "pevn_development",
"host": "127.0.0.1",
"dialect": "postgres"
},
"test": {
"username": "root",
"password": null,
"database": "pevn_test",
"host": "127.0.0.1",
"dialect": "postgres"
},
"production": {
"username": "root",
"password": null,
"database": "pevn_production",
"host": "127.0.0.1",
"dialect": "postgres"
}
}
```
