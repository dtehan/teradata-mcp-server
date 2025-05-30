
# Development Conventions

This document provides guidelines for developing new tools for the Teradata MCP server.
<br>

## Directory Structure & File Naming

The directory structure will follow the following conventions
[root directory](./) - will contain:
- README.md - this will be the main readme file, outlining scope of project, grouping of tools, installation instructions, how to use instructions.
- LICENSE file - MIT license
- pyproject.toml - Project metadata
- uv.lock - uv package lock file contains detailed package information
- .gitignore - list of files and directories that should not be loaded into github
- .python-version - python version
- env - example environments file
- custom_tools.yaml - this will enable the deployment of custom tools as defined in the yaml file.

[logs directory](./logs/) - will contain log files, the detail of the log file will be determined in the server.py file.  Default is set to INFO.  This can be changed to DEBUG for very detailed logging.

[src/teradata_mcp_server](./src/teradata_mcp_server) - this will contain all source code.
- __init__.py - will contain server imports
- server.py - contains the main server script and will decorate tools, prompts, and resources.

We will modularize the tool sets so that users will have the ability to add the tool sets that they need to the server.  It is expected that groupings of tools will have a consistent naming convention so that they can be easily associated.  

[src/teradata_mcp_server/tools/td_base](./src/teradata_mcp_server/tools/td_base) - this will contain the base tool set:
- __init__.py - will contain library imports
- td_base_tools.py - will contain the tool handle code
- td_base_prompts.py - will contain the prompt handle code
- td_base_resources.py - will contain the resource handle code
- README.md - will describe the tools, prompts, resources, and package dependencies

[src/teradata_mcp_server/tools/td_dba](./src/teradata_mcp_server/tools/td_dba) - this will contain DBA focused tools set:
- __init__.py - will contain library imports
- td_dba_tools.py - will contain the tool handle code
- td_dba_prompts.py - will contain the prompt handle code
- td_dba_resources.py - will contain the resource handle code
- README.md - will describe the tools, prompts, resources, and package dependencies

[src/teradata_mcp_server/tools/td_qlty](./src/teradata_mcp_server/tools/td_qlty) - this will contain data quality tool set:
- __init__.py - will contain library imports
- td_qlty_tools.py - will contain the tool handle code
- td_qlty_prompts.py - will contain the prompt handle code
- td_qlty_resources.py - will contain the resource handle code
- README.md - will describe the tools, prompts, resources, and package dependencies

[src/teradata_mcp_server/tools/td_fs](./src/teradata_mcp_server/tools/td_fs) - this will contain feature store (tdfs4ds package) tool set:
- __init__.py - will contain library imports
- td_fs_tools.py - will contain the tool handle code
- td_fs_prompts.py - will contain the prompt handle code
- td_fs_resources.py - will contain the resource handle code
- README.md - will describe the tools, prompts, resources, and package dependencies

**New tools sets**
New tool sets can be created in one of two ways:
1. Custom tools - this approach allows the custom_tools.yaml file to register allthe tool information.  This approach is suitable for tools that run predefined SQL against Teradata.
- using the custom_tools.yaml template 
- rename the the yaml file to the name of your tool set, ensuring that it ends in _tools.yaml
- ensure that the tool names correspond to the tool naming convention

2. New tool libraries - this approach requires changes to the server code, as defined below.
- grouping name should start with td_ and be up to 4 characters that describes the function
- Template code can be found in:
[src/teradata_mcp_server/tools/td_tmpl](./src/teradata_mcp_server/tools/td_tmpl) - this will contain template tool set:
- __init__.py - will contain library imports
- td_tmpl_tools.py - will contain the tool handle code
- td_tmpl_prompts.py - will contain the prompt handle code
- td_tmpl_resources.py - will contain the resource handle code
- README.md - will describe the tools, prompts, resources, and package dependencies

The template code should be copied and prefixes for directory name and files should be modified to align to your grouping name.  Refer to other tool sets for examples.

[src/test/](./src/test/) - this will contain client tools for testing the server functionality

[src/documentation](./src/documentation/) - contains package documentation.
- development_conventions.md - contains directory structure, file naming and tool/prompt/resource naming convention.

<br>

## Tool/Prompt/Resource Naming Convention
To assist tool users we would like to align tool, prompt, and resources to a naming convention, this will assist MCP clients to group tools and understand its function.

- tool/prompt/resource name starts with a verb and then the grouping identifier (e.g. get_td_base).
- If the tool returns data it will be a get function  (e.g.  get_td_base_)
- If the tool changes the state of data (e.g. write_td_base_)
- If a prompt (e.g. prompt_td_base)
- If a resource (e.g. resource_td_base)
- The tool/prompt/resource should have a descriptive name that is short  (e.g. get_td_base_dbList, get_td_qlty_missingValues, write_td_dba_userGrant, write_td_dba_tableCreate)

<br><br><br>

# Development Cycle

## Requesting Capabilities
- Go to github Issues tab
- click on New Issue
- click on Feature Request
- Fill out Feature Request form
    - Create a title
    - Add a description

## Raising incidents
- Go to github Issues tab
- click on New Issue
- click on Bug report
- Fill out Bug Report form
    - Create a title
    - Add a description


## Submitting Code
All contributions to the repository should be made through the Github pull request process.  

The repository admins will review the code for compliance and either provide feedback or merge the code.
