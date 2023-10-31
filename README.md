# simple_chat_app
To learn Deployment on AWS EC2

sudo apt update
sudo apt install nginx
curl -s https://deb.nodesources.com/setup_16x | sudo bash
sudo apt install nodejs
sudo npm install pm2@latest -g

mkdir ChatApp
cd ChatApp
git clone https://github.com/AwaniTests/simple_chat_app.git

cd simple_chat_app/client
npm install
cd ..
cd server
npm install
npm install express

pm2 start app.js --name chat_app

sudo vim /etc/nginx/sites_available/default

location / {
                proxy_pass http://localhost:5001;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
}

sudo nginx -t
sudo service nginx restart




