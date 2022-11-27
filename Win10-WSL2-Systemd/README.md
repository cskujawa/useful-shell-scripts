# Enable `systemd` in WSL 2

## **NOTE: If you have Windows 11 there is now an official way to do this in WSL 2, use it if possible - see MS post [here](https://devblogs.microsoft.com/commandline/systemd-support-is-now-available-in-wsl/) (*WINDOWS 11 ONLY*)**

This guide will enable `systemd` to run as normal under WSL 2. This will enable services like `microk8s`, `docker` and many more to `just work` during a WSL session. Note: this was tested on Windows 10 Build 2004, running Ubuntu 20.04 LTS in WSL 2.

- To enable `systemd` under WSL we require a tool called `systemd-genie`

- Copy the contents of `install-sg.sh` to a new file `/tmp/install-sg.sh`:

  ```bash
  cd /tmp
  curl https://raw.githubusercontent.com/cskujawa/useful-shell-scripts/main/Win10-WSL2-Systemd/install-sg.sh > install-sg.sh
  ```

- Make it executable:

  ```bash
  chmod +x /tmp/install-sg.sh
  ```

- Run the new script:

  ```bash
  /tmp/install-sg.sh && rm /tmp/install-sg.sh
  ```

- Exit the WSL terminal and shutdown the WSL env:

  ```bash
  wsl --shutdown
  ```

- To open a new WSL terminal with `systemd` enabled, run:

  ```powershell
  wsl genie -s
  ```

- Prove that it works:

  ```bash
  sudo systemctl status time-sync.target
  ```
