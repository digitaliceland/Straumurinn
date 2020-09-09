# Straumurinn
Rekstrarumhverfi Straumsins

## Preface

We recommend that you start by testing the [*Standalone Security Server*](https://github.com/digitaliceland/Straumurinn#standalone-security-server) so that you can get familiar with day-2 operations such as registering webservices enpoints.

### Standalone Security Server

We have created getting started guide on how to use [Standalone Security Server](https://github.com/digitaliceland/Straumurinn/blob/master/DOC/Manuals/standalone_security_server_tutorial.md) which runs in a container and can be executed with container runtimes such as Docker or Podman for local testing  and development. This will help you understand how to register your services in a Security Server before you start installing on IS-DEV, IS-TEST or IS.

## Getting started installing Security Server and intial configuration
Here are the steps needed to install and participate in Straumurinn (Icelandic X-Road environment).
1. Check out install guides for
    - [RedHat 7 or 8 / CentOS 7 or 8 *(Recommended)*](https://github.com/nordic-institute/X-Road/blob/develop/doc/Manuals/ig-ss_x-road_v6_security_server_installation_guide_for_rhel.md)
        1. In chapter 2.5 Installation step 1. You should use Icelandic mirror instead of Artifactory. Doing this speeds up your install.
            * Don not use: `sudo yum-config-manager --add-repo https://artifactory.niis.org/xroad-release-rpm/rhel/7/current`
            * Use instead: 
                ```
                sudo RHEL_MAJOR_VERSION=$(source /etc/os-release;echo ${VERSION_ID%.*})
                sudo yum-config-manager --add-repo https://mirrors.opensource.is/xroad/xroad-release-rpm/rhel/${RHEL_MAJOR_VERSION}/current/
                ```
        2. X-Road Package name to install in chapter 2.5, step 4 is: `xroad-securityserver-is`
        3. [AsciiMena Recording if the install procedure is here](https://asciinema.org/a/xQIsVCnYL0sq9eOKgIzddqXHB)
    - [Ubuntu 18.04 LTS](https://github.com/nordic-institute/X-Road/blob/develop/doc/Manuals/ig-ss_x-road_v6_security_server_installation_guide.md)
        1. In chapter 2.5 Installation step 2. You should use Icelandic mirror instead of Artifactory. Doing this speeds up your install.
            * Don not use: `sudo apt-add-repository -y "deb https://artifactory.niis.org/xroad-release-deb $(lsb_release -sc)-current main"`
            * Use instead: `sudo apt-add-repository -y "deb https://mirrors.opensource.is/xroad/xroad-release-deb $(lsb_release -sc)-current main"`
        2. X-Road Package name to install in chapter 2.5, step 4 is: `xroad-securityserver-is`
        3. AsciiMena Recording of the install procedure is here
2. Download Configuration Anchor for the instance you need
    - [IS-DEV - Development](Anchor/IS-DEV/configuration_anchor_IS-DEV.xml)
        - `MD5: bf31d93ef082968ff24ed7f3a7dc20e8`
    - [IS-TEST - Testing](Anchor/IS-TEST/configuration_anchor_IS-TEST.xml)
        - `MD5: f9a682420b33328267ed66da3ca38f31`
    - [IS - Production](Anchor/IS/configuration_anchor_IS.xml)
        - `MD5: 53679813b9d1dfa2607756d482ee76e2`
3. Next steps invole in logging into the admin interface located at https://servername:4000 and initalize the server using the correct Configuration Anchor above.

## Network Whitelist

When you are installing Security Server you probably have to do some firewall openings. [Network Whitelist](https://github.com/digitaliceland/Straumurinn/blob/master/DOC/Manuals/ig-ss-security_server_install_guide.md) and what ports need to be open is located here.
