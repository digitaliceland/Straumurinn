# Straumurinn
Rekstrarumhverfi Straumsins

## Getting started
Here are the steps needed to install and participate in Straumurinn (Icelandic X-Road environment).
1. Check out install guides for
    - [RedHat 7 / CentOS 7 *(Recommended)*](https://github.com/nordic-institute/X-Road/blob/develop/doc/Manuals/ig-ss_x-road_v6_security_server_installation_guide_for_rhel7.md)
        1. In chapter 2.5 Installation step 1. You should use Icelandic mirror instead of Artifactory. Doing this speeds up your install.
            * Don not use: `sudo yum-config-manager --add-repo https://artifactory.niis.org/xroad-release-rpm/rhel/7/current`
            * Use instead: `sudo yum-config-manager --add-repo https://mirrors.opensource.is/xroad/xroad-release-rpm/rhel/7/current/`
        2. X-Road Package name to install in chapter 2.5, step 4 is: `xroad-securityserver-is`
        3. [AsciiMena Recording if the install procedure is here](https://asciinema.org/a/xQIsVCnYL0sq9eOKgIzddqXHB)
    - [Ubuntu 18.04 LTS](https://github.com/nordic-institute/X-Road/blob/develop/doc/Manuals/ig-ss_x-road_v6_security_server_installation_guide.md)
        1. In chapter 2.5 Installation step 2. You should use Icelandic mirror instead of Artifactory. Doing this speeds up your install.
            * Don not use: `sudo apt-add-repository -y "deb https://artifactory.niis.org/xroad-release-deb $(lsb_release -sc)-current main"`
            * Use instead: `sudo apt-add-repository -y "deb https://mirrors.opensource.is/xroad/xroad-release-deb $(lsb_release -sc)-current main"`
        2. X-Road Package name to install in chapter 2.5, step 4 is: `xroad-securityserver-is`
        3. AsciiMena Recording if the install procedure is here
2. Download Configuration Anchor for the instance you need
    - [IS-DEV - Development](https://github.com/digitaliceland/Straumurinn/Anchor/IS-DEV/configuration_anchor_IS-DEV.xml)
        - `MD5: bf31d93ef082968ff24ed7f3a7dc20e8`
    - [IS-TEST - Testing](https://github.com/digitaliceland/Straumurinn/Anchor/IS-TEST/configuration_anchor_IS-TEST.xml)
        - `MD5: f9a682420b33328267ed66da3ca38f31`
    - [IS - Production](https://github.com/digitaliceland/Straumurinn/Anchor/IS/configuration_anchor_IS.xml)
        - `MD5: 53679813b9d1dfa2607756d482ee76e2`
3. Next steps invole in logging into the admin interface located at https://servername:4000 and initalize the server using the correct Configuration Anchor above.

## Network Whitelist

When you are installing Security Server you probably have to do some firewall openings. [Network Whitelist](https://github.com/digitaliceland/Straumurinn/blob/master/DOC/Manuals/ig-ss-security_server_install_guide.md) and what ports need to be open is located here.

## Standalone Security Server

You can check out our getting started guide on [Standalone Security Server](https://github.com/digitaliceland/Straumurinn/blob/master/DOC/Manuals/standalone_security_server_tutorial.md) running on Docker for local testing before you start installing on IS-DEV, IS-TEST or IS. We recomment doing this first before starting to install anything.