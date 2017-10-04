#website on WWW hosted by heroku
https://sfun.herokuapp.com/
# website url on cloud 9
# first start mongoDB (in same directory as data folder and mongod* folder)
./mongod
#start server
node app.js
workspacename-username.c9users.io
http://webdevelopment-stellaryoshi.c9users.io/

#set up:
npm init
# install dependencies
npm install --save body-parser connect-flash ejs express express-session 
method-override mongoose passport passport-local passport-local-mongoose

#install MongoDB on cloud 9
sudo apt-get install -y mongodb-org
#in cloud9, mongoDB data folder is in webdevelopment folder
mkdir data
echo 'mongod --bind_ip=$IP --dbpath=data --nojournal --rest "$@"' > mongod
chmod a+x mongod
#start mongoDB (in same directory as data folder and mongod* folder)
./mongod
# leave terminal with mongod open and use different terminal. Cntrl+c to close.

#If you leave it running then Cloud 9 could timeout and cause mongo to crash. 
#If this happens, try the following steps to repair it. From the command line, run:

cd ~
./mongod --repair


#deploy to heroku
#make sure in package.json, you have all dependencies listed, 
#and under "scripts" : {"start": "node app.js"}
# in website folder cloud 9 terminal
# heroku installed, checking version
heroku -v
git init
#add to git all files
git add .
git commit -m "initial deploy"
heroku create #do only once when  first time creating heroku app
git push heroku master

#update website name hosted on heroku
git init
git add .
git commit -m "URL changed"
git push heroku master

heroku apps:rename <newname>
#OR you renamed the website on heroku user site, then
git remote rm heroku
heroku git:remote -a <newname>



#run on heroku terminal
heroku run <terminal command>
#eg, check installed packages
heroku run ls node_modules
heroku run npm install <package-name> --save

#host your MongoDB online at  www.mlab.com
#deploy new db and add db user who can access db
mongodb://<dbuser>:<dbpassword>@dsport.mlab.com:port/website_on_heroku

#set the process environment variable DATABASEURL in app.js by:
#go to heroku user website, settings-> configure variable, add: 
KEY= DATABASEURL
VALUE=mongodb://<dbuser>:<dbpassword>@dsport.mlab.com:port/website_name
#OR run in cloud9 command terminal
heroku config:set DATABASEURL=mongodb://<dbuser>:<dbpassword>@dsport.mlab.com:port/website_name
#note: DO NOT put address of DATABASEURL in your code, if shown/open source someone can steal & use your db

#Add images from unsplash.com
find photoID from after ?photo=
<img src="https://source.unsplash.com/<photoID>">