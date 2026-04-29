
Container 3

git clone https://github.com/rhavymaia/minhaappweb20252.git

cd minhaappweb20252/

npm install

npm run build

cd /etc/nginx/sites-available

vim minhaappweb20252.conf

cd ../sites-enabled/

ln -s /etc/nginx/sites-available/minhaappweb20252.conf /etc/nginx/sites-enabled/

vim nginx.conf 

	#user www-data;
	user root;

vim sites-available/minhaappweb20252.conf

server {
    listen 80;                          # Listen for HTTP traffic on port 80
    server_name _; # Domains this block handles
    root /home/ubuntu/minhaappweb20252/dist;             # Directory containing website files
    index index.html;     # Default files to serve

    location / {
        # Esta linha é a mais importante:
        # Tenta servir o arquivo original, depois diretórios,
        # e se não encontrar, passa para o index.html (SPA)
        try_files $uri $uri/ /index.html;
    }

}


systemctl stop nginx

systemctl start nginx