# ansible-web

## Introduction
Deploying has something very repetitive and painful. Create a domain, clone project, install
dependencies, etc. I built this to help me deploy things faster.

## Requirements
Make sure you have the following dependencies installed

- ansible
- git

As an additional requirement, you need to have a root user in the server you'll deploy, and you
need to be able to log in with that user via ssh.

## How to use
Review the playbooks, and edit accordingly, maybe you'll not need to build your project every time
or there's some missing task.

### First run
Only use this playbook **once per server**. It'll create an SSH key and a new user in your server.

1. Replace the variables marked between `<>` in `playbooks/groups/firstrun.yml`
2. Update the `./hosts` file to something like
  ```sh
  [foo]

  foo.com
  ```
3. Run the playbook
  ```sh
  ansible-playbook -i hosts playbooks/groups/firstrun.yml
  ```

  ### Preparations per domain
  1. Make sure you don't publish private information, I'd recommend deleting the `.git` folder just
  to be sure.
  2. Rename `your_domain_.com*` files to resemble your domain, i.e. `foo.com.yml`
  3. Replace the <your_hosts> to the host you created in `./hosts`, i.e. `foo`.
  4. Replace the <your_domain.com> to your actual domain, i.e. `foo.com`

### First deploy
Run this playbook **only when deploying a project for the first time**. It'll configure the
`nginx` domain in your server, and install all required dependencies

```sh
ansible-playbook -i hosts playbooks/groups/<your_domain.com_first_deploy.yml>
```

### Deploy a new version
Run this whenever you have an update for your code and need to deploy.

```sh
ansible-playbook -i hosts playbools/groups/<your_domain.com.yml>
```
