# Caddy-HomelabDemo
Reverse proxy via config files.

## Things to note in a deployment of this tool
- this is a DEMO, please see FAQ section of README
- Containers like Caddy that have a configuration file, require a reboot of the container to pull in the changes.
- Ensure bind mounts on host are set to 600 permissions (rw-------), and have the correct owner/group to align with uid/gid given to container space.
- I tend to avoid wildcard certs, while quick and simple in a homelab, I prefer to mitigate attack surface and treat my homelab close what would be in an enterprise prod setup.
- Caddyfile is setup as if all my homelab demos were being deployed.
- Caddy expects you to call out two file paths when calling preloaded certs, I break out my key and cert in this demo for easy of understanding. Both can be in one file, even though you call it twice.
- I use a .env file to set a variable in the Caddyfile, this is an example for demo purposes and would be better set via a secret in a swarm or through a ci/cd variable.

## Prerequisite in a deployment of this exact repo
- Gitlab and a runner are Deployed and configured to talk to target server
- Some Variables have been configured within Gitlab to inject into a pipeline at runtime
- target server at a minimum has docker and openssh server (w/ .pub key) setup
- DNS resolver is already configured
- Updating .env file for your needs
- You have a domain name and are using dns validation with Cloudflair, and have an API token setup

## Resources:
- github: https://github.com/caddyserver/caddy
- website: https://caddyserver.com/
- Documentation: https://caddyserver.com/docs/

## FAQ for repo visitors
### Why does the repo have 'Demo' in the title?
this "demo" repo is based on real world local deployments in my Homelab. Some settings may be changed, or different for privacy and safety.

### Why a gitlab pipeline file (.gitlab-ci.yml)?
I selfhost a Gitlab instance at home for experimentation, experience and privacy. So I use gitlab runners to deploy my pipelines, this is the native file for that. In the future I will update these demos to reflect github native pipelines workflows (.github/workflows/PIPELINE.yml), or maybe I'll do a jenkins demo for my own learning.

### Why multiple branches
I have a test and main branch to more demo a enterprise setup, where you might have people pushing changes to a protected test branch that is then has pipelines to stage tooling in a test space. Which once pulled into main, would deploy the same setup to PROD.

### Why Caddy over 'Traefik', 'HAproxy', 'Nginx proxy manager', etc?
I have tried a few different proxy managers, but settled in Caddy for the straightforward nature and ability to quickly configure via file allowing for a IaC deployed Reverse Proxy.

### Where can I find more about this project and your thought process?
I make it a habit that my files typically have dozens of in-line comments to better help anyone using them for the first time to understand what is happening, maybe not always why. Also please check out my blog, it typically has more information on my projects (sometimes the post is still being planned).

### Does ths connect to your other Homelab Demo repos?
yes! for the most part this will be siloed, but most of these demos connect to this exact project.

### Was AI used to generate this?
No, but I have learned and expanded my knowledge of the tools within this project with AI. AI I see as a tool and resource that is loose in the market place regardless of your stance, that you need to follow, know how to use, while educating others and putting safeguards around it. I firmly lead with my own brainstorming, knowledge, design and troubleshooting first for my deployments, but i have used AI to troubleshoot, help expand understanding, research, and experimented with vibe coding. 

## Issues to note with this "demo"
I wanted to do a proper code repo that could be poke around so you could see commits and pulls that you might normally see in a team production repo, unfortunately due to the overhead and this [issue](https://github.com/orgs/community/discussions/6292), I will be "cutting corners" and doing everything locally then pushing to main directly from my machine. However, I will still leave the demo "main" and "test" branches with there protections.

## Docker features, CI/CD tooling/skills, and other tools leveraged in this project.
- Docker:
    - image pull
    - compose
    - Networking
    - bind mounts and volumes
    - device passthrough
    - Permissions (capabilities)
    - environment variables
    - managing tooling multiple configurations files
- Yaml
- Git
- Gitlab interface and secret management
- Pipelines (all in Gitlab formatting)
- Git CD/CI best practices (branches, branch protections, etc)
- Linux (general and permissions)
- Bash
- SSH
- Documentation