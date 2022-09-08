# ubuntu

ubuntu environments

## for container
keep your container alive via jupyterlab
```
apt update;  apt install -y python3-pip;  pip3 install jupyterlab;  mkdir -p /workspace;  jupyter-lab --allow-root --ip 0.0.0.0 --ServerApp.token='' --ServerApp.password='' --notebook-dir=/workspace --no-browser
```

