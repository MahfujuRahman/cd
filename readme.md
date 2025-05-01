First Login to Aapanel

create a project repository

one time setup - if git not installed then 
run git install

and 
Step 1: On your VPS, generate a new SSH key (if not already created)

ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/ajmain

Step 2: Copy the public key
cat ~/.ssh/ajmain.pub
and copy

cat ~/.ssh/ajmain.pub >> ~/.ssh/authorized_keys

Go to: GitHub → Settings → SSH and GPG keys

Click New SSH key

Title: VPS

Paste the key you copied

Save

ssh -T git@github.com


cd /www/wwwroot/test.mirpurianscafe.com
git clone git@github.com:MahfujuRahman/cd.git .


after that inyour project make .github/workflows/deploy.yml

name: Blood  Management

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Deploy using ssh
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.VPS_HOST }}
          username: ${{ secrets.VPS_USER }}
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          port: 22
          script: |
            # Navigate to project directory
            cd ${{ secrets.PROJECT_PATH }}

            # Pull the latest code
            git pull origin main

            # # Install dependencies and build the project
            # npm install
            # npm run build

and in your project


🔐 3. Add Private Key to GitHub Secrets
Go to GitHub Repo > Settings > Secrets and Variables > Actions and add:

Name	Value
SSH_PRIVATE_KEY	Content of github-actions (the private key)
VPS_HOST	Your VPS IP (e.g., 20.2.4.20)
VPS_USER	The username you use to SSH (e.g., root)
PROJECT_PATH	Full path to your Laravel project on VPS (e.g., /www/wwwroot/yourdomain.com)


no