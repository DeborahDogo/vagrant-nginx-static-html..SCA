Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "private_network", ip: "192.168.56.40"
  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1600"
  end

  config.vm.provision "shell", inline: <<-SHELL

    # Step 1: Update package list and install Nginx
    sudo apt update -y
    sudo apt install nginx -y

    # Step 2: Create a simple custom HTML page in the default web root
    cat > /var/www/html/index.html <<'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hello Nginx</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; padding: 80px 20px; background: #f8f9fa; }
    h1   { color: #2c5282; }
    .ip  { color: #e53e3e; font-weight: bold; }
  </style>
</head>
<body>
  <h1>Hello from Nginx!</h1>
  <p>This is a simple static page served by Nginx in Vagrant.</p>
  <p>IP: <span class="ip">192.168.56.40</span></p>
</body>
</html>
EOF

    # Step 3: Ensure Nginx is enabled to start on boot
    sudo systemctl enable nginx 

    # Step 4: Restart Nginx to load the new page
    sudo systemctl restart nginx

    # Step 5: verify that Nginx is running
    # You can uncomment the next line during troubleshooting
    # systemctl status nginx

    # Step 6:Show a confirmation message in the provisioning log
    echo "Nginx provisioning completed. Visit http://192.168.56.40"

  SHELL
end
