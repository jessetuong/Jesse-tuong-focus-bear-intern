## Docker vs. virtual machines

- VMs virtualize an entire machine, and each VM runs its own kernel, making them heavy and slow to boot
- Docker containers share the host machine's OS kernel and only package the app plus its dependencies which is much lighter (MBs), start in seconds
- VMs have more isolation; containers are faster, more efficient isolation at the process level

## Why containerization is useful for a backend like Focus Bear's

- The container includes the exact runtime, libraries, and config needed
- Makes onboarding new developers faster by preventing them from manually installing every dependencies
- Reduce environment-specific bugs, which keep dev, staging and production environments consistent
- Makes it easy to run multiple services together via docker-compose without conflicts on the host machine

## How containers help with dependency management

- Each container bundles its exact dependency versions, isolated from other projects on the same machine, which reduce the chance of dependency conflicts
- Removes the need to install project dependencies directly on your host OS at all
- Avoid breaking local setups (folders, dependencies) since Dockers help grouping and isolating the dependencies needed in 1 enviroment

## Potential downsides of Docker

- Learning curve — Dockerfiles, images, volumes, and networking add complexity beyond just running code directly
- Slight performance overhead compared to running natively (though far less than a VM)
- Debugging inside containers can be less intuitive (extra steps to attach a debugger, inspect logs, or access files)
- Requires Docker itself to be installed, which requires users to spend time installing and learning how to use it