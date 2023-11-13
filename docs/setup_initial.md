# Initial Setup 

This note covers every steps needed to set up a machine and connect it gcloud


## Google Cloud Website Instance Creation
1. login on the google cloud webpage 
2. click `Console` on the top right corner
3. Search `Compute Engine` in the search bar
4. Click `CREATE INSTANCE` below the Compute Engine
    1. Boot disk to pick os (can use the default deep learning disk)
    2. Enable http, https connection 


## Connecting to the instance from terminal
1. Install gcloud suite from the website
2. Run `gcloud auth login`
3. On the webpage `Compute Engine` page, right next to the instance, click
`View gcloud command`
4. Run the command `gcloud compute ssh --zone "us-east1-d" "instance-1" --project "arctic-kiln-391812"`

## GUI through xquartz forwarding
This is the most complicated side on the setup. I will divide the contents into three sections: 
- server side, which is the setup on the google cloud instance
- client side, which is the setup on the mac that's connecting to the instance
- clipboard, particular setup for clipboard


### Client side
`brew install xquartz`
Override all xquartz short keys by going to System Preferences -> Keyboard -> Shortcuts -> App Shortcuts -> add application -> utilities / xquartz map the exact name on the menu item
To make sure the ssh connect enable X11Forwarding, add `-- -X` at the end of gcloud command. For example
`gcloud compute ssh --zone "us-east1-d" "instance-1" --project "arctic-kiln-391812" -- -X`

## Server setup 
1. After login onto the instance, run `sudo apt-get update`
1. We first need to enable the x11 forwarding. A useful webpage is [here](https://myshittycode.com/2022/02/23/gcp-accessing-gui-based-software-in-gce-from-mac-using-x11).   At this point, we should be able to login the compute engine through mac terminal. And we should be able to use applications with gui. The next steps are the server configurations 
2. Install zsh and [oh-my-zsh](https://ohmyz.sh). Change theme to `ZSH_THEME="maran"` 
3. Install neovim through appimage at [here](https://github.com/neovim/neovim/wiki/Installing-Neovim)
3. `sudo apt-get install neovim-qt`.
4. Go to `/usr/bin`, delete the nvim, and then create a symbolic link to latest neovim appimage
5. Add git permsion [tokens](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
4. Go to `~/.config` and `clone sigcyc/nvim`
5. Install [micromamba](https://mamba.readthedocs.io/en/latest/micromamba-installation.html#umamba-install)
6. `micromamba install jax` and `micromamba install jupyter`, put `micromamba activate sigcyc1` at the end of `~/.zshrc`

## Set GPU quota
By default, the account will allow 0 GPUs to 
1. Search `IAM & Admin`
2. Click `Quota` on the right side
3. Differnt from the webpage, type `Metrics` first, and then type `gpus_all_regions`
See [here](https://www.reddit.com/r/cloudygamer/comments/agzh9w/how_to_fix_google_cloud_gpu_quota_issue/?onetap_auto=true)


## Install CUDA
Follow the script [here](https://cloud.google.com/compute/docs/gpus/install-drivers-gpu)
To check the cuda version, run `nvidia-smi`
Install jax with cuda support, follow [here](https://jax.readthedocs.io/en/latest/installation.html)

## Useful notes
1. It might be easy to check the manual. e.g, I fixed the bug on the forwarding by checking the manual 
`gcloud compute ssh --help`
2. Getting a prompt that doesn't show the environment name
Check carefully if .zshrc has set `prompt adam1` somewhere
