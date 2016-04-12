---
UID: 56f98449e7e89
post_title: Command Line Interface
post_excerpt: ""
layout: docs.jade
published: true
menu_order: 2
page_options_require_authentication: false
page_options_show_link_unauthenticated: false
hide_from_navigation: false
hide_from_related: false
---
You can use the Mesosphere DCOS command-line interface (CLI) to manage your cluster nodes, install DCOS packages, inspect the cluster state, and administer the DCOS service subcommands. You can install the CLI from the DCOS web interface.

To list available commands, either run `dcos` with no parameters or run `dcos help`:

    $ dcos
    Command line utility for the Mesosphere Datacenter Operating
    System (DCOS). The Mesosphere DCOS is a distributed operating
    system built around Apache Mesos. This utility provides tools
    for easy management of a DCOS installation.
    
    Available DCOS commands:
    
        config          Get and set DCOS CLI configuration properties
        help            Display command line usage information
        marathon        Deploy and manage applications on the DCOS
        node            Manage DCOS nodes
        package         Install and manage DCOS packages
        service         Manage DCOS services
        task            Manage DCOS tasks
    
    Get detailed command description with 'dcos <command> --help'.
    

# Environment Variables

For easy reference, these environment variables are supported by the DCOS command line:

The DCOS CLI supports several environment variables that you can set dynamically.

`DCOS_CONFIG` Set the path to the DCOS configuration file. By default, this variable is set to `DCOS_CONFIG=/<home-directory>/.dcos/dcos.toml`. For example, if you moved your DCOS configuration file to `/home/jdoe/config/` you can specify this command:

    $ export DCOS_CONFIG=/home/jdoe/config/dcos.toml
    

`DCOS_SSL_VERIFY` Indicates whether to verify SSL certificates for HTTPS (`true`) or set the path to the SSL certificates (`false`). By default, this is variable is set to `true`. This is equivalent to setting the `core.ssl_config` option in the DCOS configuration file. For example, to set the path to SSL certificates:

    $ export DCOS_SSL_VERIFY=false
    

`DCOS_LOG_LEVEL` Prints log messages to stderr at or above the level indicated. This is equivalent to the `--log-level` command-line option. The severity levels are:

*   **debug** Prints all messages to stderr, including informational, warning, error, and critical.
*   **info** Prints informational, warning, error, and critical messages to stderr.
*   **warning** Prints warning, error, and critical messages to stderr.
*   **error** Prints error and critical messages to stderr.
*   **critical** Prints only critical messages to stderr.

For example, to set the log level to warning:

    $ export DCOS_LOG_LEVEL=warning
    

`DCOS_DEBUG` Indicates whether to print additional debug messages to `stdout`. By default this is set to `false`. For example:

    $ export DCOS_DEBUG=true
    

# Configuration Files

By default, the DCOS command line stores its configuration files in a directory called `~/.dcos` within your HOME directory. However, you can specify a different location by using the `DCOS_CONFIG` environment variable.

The configuration settings are stored in the `dcos.toml` file. You can modify these settings with the `dcos config` command.

**dcos_acs_token** This is the token generated by authenticating to DCOS with ACS. This is set by default during installation. For example:

    dcos config set core.dcos_acs_token 
    

For more information about security and authentication, see the [documentation][1].

**dcos_url** The the public master IP of your DCOS installation. This is set by default during installation. For example:

    dcos config set core.dcos_url 52.36.102.191
    

**email** Your email address. This is set by default during installation. For example, to reset your email address:

    dcos config set core.email jdoe@mesosphere.com
    

**mesos_master_url** The Mesos mast URL. This must be of the format: `http://<host>:<port>`. For example, to set your Mesos master URL:

    dcos config set core.mesos_master_url 52.34.160.132:5050
    

**reporting** Indicate whether to report usage events to Mesosphere. By default this is set to `True`. For example, to set to false:

    dcos config set core.reporting=False
    

**ssl_verify** Indicates whether to verify SSL certs for HTTPS or path to certs. By default this is set to `False`. For example, to set to true:

    dcos config set core.ssl_verify=True
    

**timeout** Request timeout in seconds, with a minimum value of 1 second. By default this is set to 5 seconds. For example, to set to 3 seconds:

    dcos config set core.timeout=3
    

**token** The OAuth access token. For example, to change the OAuth token:

    dcos config set core.token <token>

 [1]: /administration/security-and-authentication/