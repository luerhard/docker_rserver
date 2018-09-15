# Docker Rserver for Multiuser-setup 
This Dockerfile runs a rserver and contains a script for super simple user addition on the server. All users share the .libPaths(), are allowed to install packages but have separate working directories.

# Usage
If needed add wanted packages in the install_packages.R. They will be installed on build-time.
Build with `build . -t rserver`, then run with:
```
docker run -d -p port_on_host:8787 -v /path/on/host:/home --name rstudio_server rserver
```
make sure everyone has write-access on the /path/on/host folder. `chmod -R 777 /path/on/host` for example.

# Root-User
There is a root user named rstudio that comes with this installation. The default password ist 'password'. Make sure to go to the terminal in RStudio and type `passwd` on the first login to change to root password.

# Add User
Only the user rstudio can add new users. To add new a new user log in as rstudio, go to the terminal and type:
```
sudo bash /usr/new_user.sh new_user_name user_password
```
to create a new user `new_user_name` with the password `user_password`. Make sure to tell all new users to change their password immediatly as explained in section "Root-User".

## rocker/rstudio-stable
A large part of the Dockerfile ist copied from rocker/rstudio-stable.
