# Initial Setup 

This note covers every steps needed to set up a machine and connect it gcloud


## Google Cloud Website Instance Creation
1. login on the google cloud webpage 
2. click `Console` on the top right corner
3. Search `Compute Engine` in the search bar
4. Click `CREATE INSTANCE` below the Compute Engine
    1. Boot disk to pick os
    2. Enable http, https connection 
5. After login onto the instance, run `sudo apt-get update`


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

### Server side
We first need to enable the x11 forwarding. A useuul webpage is [here](https://myshittycode.com/2022/02/23/gcp-accessing-gui-based-software-in-gce-from-mac-using-x11)

### Client side
`brew install xquartz`
Override all xquartz short keys by going to System Preferences -> Keyboard -> Shortcuts -> App Shortcuts -> add application -> utilities / xquartz map the exact name on the menu item
To make sure the ssh connect enable X11Forwarding, add `-- -X` at the end of gcloud command. For example
`gcloud compute ssh --zone "us-east1-d" "instance-1" --project "arctic-kiln-391812" -- -X`

## Server setup after GUI
At this point, we should be able to login the compute engine through mac terminal. And we should be able to use applications with gui. The next steps are the server configurations 
1. install zsh, and put zsh in the bashrc
2. Install neovim. Go to `~/.config` and `clone sigcyc/nvim`


## Useful notes
1. It might be easy to check the manual. e.g, I fixed the bug on the forwarding by checking the manual 
`gcloud compute ssh --help`

