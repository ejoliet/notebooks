This needs to be ran locally for now, and this is still in progress.

Steps to upload a distributable version of pylibamazed:
- Pyserver is needed

Run a pyserver using docker image:

`docker run -p9095:8080 pypiserver/pypiserver:latest`

Access PyPi.org server via localhost:9095 or HOST_IP:9095

The pylibamazed package (tar) generated should have been uploaded previously. 
If package is under ~/packages, run with `-v ~/python_packages:/data/packages` to map the packages data folder from the host into the container before running pyserver (https://github.com/pypiserver/pypiserver#using-the-docker-image)

- Build C++ and Python pylibamazed, see https://github.com/IPAC-SW/roman-gdps-lam
- Once built, go to pylibamazed folder and make a dist of the python package to be uploaded
    `python setup.py sdist`
- the result tar is under dist folder
- copy this out to the host from the container
`dr cp <CONTAINER_ID>:/root/roman-gdps-lam/pylibamazed/dist/pylibamazed-0.20.1.tar.gz python_packages/`
- or find the way to upload to the pypi server (not yet working because auth failing):
`python3 setup.py sdist upload -r local`, where 'local' is defined under ~/.pypirc

