# Running an nginx web server on a Linux VM (Debian)

# Step 1: Installing nginx Linux VM:

A: Following nginx documentation on nginx.org, installing prerequisites for NGINX:

```bash
$ sudo apt install curl gnupg2 ca-certificates lsb-release debian-archive-keyring
```

B: Importing official signing key:

```bash
$ curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
```

C: Verifying signing key: 

```bash
$ gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
```

D: Set up stable packages:

```bash
$ echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
http://nginx.org/packages/debian `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list
```

E: Pinning nginx packages over distribution-provided ones:

```bash
$ echo -e "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | sudo tee /etc/apt/preferences.d/99nginx
```

F: Install nginx:

```bash
$ sudo apt update
$ sudo apt install nginx
```

E: Checking status of nginx:

```bash
$ sudo service nginx status
# server inactive
```

Issue 1: server inactive

Solution to issue 1: start the server

```bash
$ sudo service nginx start
# server active and running
```
