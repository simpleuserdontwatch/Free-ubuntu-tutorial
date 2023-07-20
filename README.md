# Free-ubuntu-tutorial
Heres a way how to get ubuntu for free without buying 2nd computer or spending storage on an ubuntu image
1. Create new repo
2. Create new workflow with this contents:
```yaml
name: CI
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Update enviroment
        run: sudo apt-get update -y
      - name: Download chrome desktop remote to /tmp
        run: wget https://dl.google.com/linux/direct/chrome-remote-desktop_current_amd64.deb -P /tmp
      - name: Download chrome desktop using apt
        run: sudo apt install /tmp/chrome-remote-desktop_current_amd64.deb --fix-missing
      - name: Adding new user named vm
        run: sudo useradd vm
      - name: Changing DISPLAY variable to chrome remote desktop one
        run: "DISPLAY= /opt/google/chrome-remote-desktop/start-host --code='Code here' --redirect-url='https://remotedesktop.google.com/_/oauthredirect' --name='GITHUB' --user-name=vm --pin=123456"
      - name: Download shell
        run: sudo apt install ubuntu-gnome-desktop
      - name: Mainloop
        run: "sleep 941480149401"
```
3. Navigate to [chrome remote desktop headless setup](https://remotedesktop.google.com/headless)
4. Press start then next then authorize
5. You should get a few of text boxes, Copy the code of one of textboxes which starts with `4/` or any other
6. Replace Code here with your copied text
7. Now run workflow and you are done
