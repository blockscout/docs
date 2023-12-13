# Ubuntu Setup

### 1. Install Requirements

1. `sudo apt-get update`
2. `sudo apt-get install inotify-tools && sudo apt install make && sudo apt install g++`
3. `sudo apt-get install libudev-dev zip unzip build-essential cmake -y`
4. `sudo apt-get install git`\
   `automake`\
   `libtool inotify-tools`\
   `libgmp-dev`\
   `libgmp10`\
   `build-essential`\
   `cmake -y`

### 2. Install ASDF

1. `git clone https://github.com/asdf-vm/asdf.git ~/.asdf`
2. Edit your ubuntu profile\
   &#x20;`nano .profile`&#x20;
3. add this line in end break \
   &#x20;`. $HOME/.asdf/asdf.sh`  and ctrl + x (or Save)
4. Refresh your profile after the update \
   &#x20;`. ~/.profile`&#x20;
5. `add plugin asdf`
6. `asdf plugin add erlang`
7. `asdf plugin add elixir`
8. `asdf plugin add nodejs`
9. install additional prerequisites\
   `sudo apt-get -y install build-essential autoconf m4 libncurses5-dev libwxgtk3.0-gtk3-dev libwxgtk-webview3.0-gtk3-dev libgl1-mesa-dev libglu1-mesa-dev libpng-dev libssh-dev unixodbc-dev xsltproc fop libxml2-utils libncurses-dev openjdk-11-jdk`&#x20;

### 3. Install PostgreSQL-14

1. `curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg`
2. `sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'`
3. `sudo apt update`
4. `sudo apt install postgresql-14`
5. `sudo systemctl status postgresql-14`

### 4. Add user and database in postgres-14

1. `adduser dbusername` \
   **Note:** Replace dbusername with your username.
2. You will be prompted to create a new profile, just follow the flow.
3. After Adduser now connect to postgres-14\
   `su - postgres` (for Root) or `sudo -i -u postgres` (for user)
4. Create user\
   `createuser --interactive dbusername`&#x20;
5. Create database\
   `createdb blockscout`&#x20;
6. connect to psql\
   `psql`
7. `ALTER USER dbusername WITH PASSWORD 'dbuserpassword';` < Replace dbusername and dbuserpassword that you created
8. `GRANT ALL PRIVILEGES ON DATABASE blockscout TO dbusername;` < Replace dbusername
9. exit psql\
   `\q`
10. Restart postgresql\
    `sudo systemctl restart postgresql`&#x20;
11. Check the new profile that you created at the start of adduser replaceing dbusername with your username.\
    `su - dbusername` (for Root) or `sudo su - dbusername` (for user)&#x20;
12. Run this command\
    `psql -d blockscout`
13. If everything is correct, you will see this response `=#`
14. Quite psql\
    &#x20;`\q`&#x20;

{% hint style="success" %}
### 🎉  You are ready for [manual deployment!](./)
{% endhint %}
