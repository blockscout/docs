# Ubuntu Setup

### 1. Install Requirements

1. `sudo apt-get update`
2. `sudo apt-get install inotify-tools && sudo apt install make && sudo apt install g++`
3. `sudo apt-get install libudev-dev zip unzip build-essential cmake -y`
4. `sudo apt-get install git \`\
   `automake \`\
   `libtool inotify-tools \`\
   `libgmp-dev \`\
   `libgmp10 \`\
   `build-essential \`\
   `cmake -y`

### 2. Install ASDF

1. Clone ASDF Plugin

> git clone https://github.com/asdf-vm/asdf.git \~/.asdf

2. Edit your ubuntu profile

> nano .profile

3. add this line in end break

> . $HOME/.asdf/asdf.sh and ctrl + x (or Save)

4. Refresh your profile after the update

> source \~/.profile

5. Test active asdf after refresh

> asdf version
>
> v0.13.1-fad23bc\
> **Note**: Response following successful install

6. Add asdf plugin for erlang, elixir, and nodejs

> asdf plugin add erlang
>
> asdf plugin add elixir
>
> asdf plugin add nodejs

7. install additional prerequisites

> sudo apt-get -y install build-essential autoconf m4 libncurses5-dev libwxgtk3.0-gtk3-dev libwxgtk-webview3.0-gtk3-dev libgl1-mesa-dev libglu1-mesa-dev libpng-dev libssh-dev unixodbc-dev xsltproc fop libxml2-utils libncurses-dev openjdk-11-jdk

### 3. Install PostgreSQL-14

1. `curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg`
2. `sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'`
3. `sudo apt update`
4. `sudo apt install postgresql-14`
5. `sudo systemctl status postgresql`

### 4. Add user and database in postgres-14

1. Create user on localpc or server

> adduser dbusername\
> **Note:** Replace dbusername with your username.

2. You will be prompted to create a new profile, just follow the flow.
3. After Adduser now connect to postgres-14

> &#x20;su - postgres (for Root) or sudo -i -u postgres (for user)

4. Display when entering postgres user section looks like this in terminal

> postgres@ubuntu:\~$

5. Create user

> createuser --interactive dbusername

6. Create database

> createdb blockscout

7. connect to psql

> psql

8. Create Password database in dbusername Note

> ALTER USER dbusername WITH PASSWORD 'dbuserpassword'; \
> **Note**: Replace dbusername and dbuserpassword that you created

9. Create Privileges on dbusername to database

> GRANT ALL PRIVILEGES ON DATABASE blockscout TO dbusername;&#x20;
>
> **Note:** Replace dbusername

10. exit psql

> \q

11. Exit to profile postgresql

> postgres@ubuntu:\~$ exit

11. Restart postgresql

> sudo systemctl restart postgresql

12. Check new profile that you created at start of adduser replaceing dbusername with your username.

> su - dbusername (for Root) or sudo su - dbusername (for user)\
> **Note**: Replace your dbusername

13. Run this command

> &#x20;psql -d blockscout

14. If everything is correct, you will see this response&#x20;

> &#x20;blockscout=#

15. Quit psql

> \q

15. Exit for Database Account page

> dbusername@ubuntu:\~$ exit

### 5. After installing everything, clone the Blockscout repository and install .tool-version from the repository

1. Clone Repository Blockscout

> git clone https://github.com/blockscout/blockscout blockscout-backend

1. Enter to folder clone blockscout

> cd blockscout-backend

1. Install plugin requirements Erlang, Elixir, and Nodejs before install blockscout backend

> asdf install

{% hint style="success" %}
**🎉 You are ready for manual deployment!** [**Proceed to step 3 in the "Prepare the Backend section**](./#1.-prepare-the-backend)**"**
{% endhint %}
