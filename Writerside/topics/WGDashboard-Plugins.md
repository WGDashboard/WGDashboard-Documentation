# WGDashboard Plugins

For list of available plugins: [WGDashboard/WGDashboard-Plugins](https://github.com/WGDashboard/WGDashboard-Plugins)

## Requirements
WGDashboard v4.3+

## How to install
1. Using `git clone https://github.com/WGDashboard/WGDashboard-Plugins.git` or download the repo with this [link](https://github.com/WGDashboard/WGDashboard-Plugins/archive/refs/heads/main.zip)
2. Copy the plugin folder you want into `WGDashboard/src/plugins`
3. Restart WGDashboard to load the new plugin

## How WGDashboard load plugins?

```mermaid
flowchart TD
        A(["WGDashboard Startup"])
        A --> B{"if ./plugins exist"}
        B -- true --> C["Loop through directories in ./plugins"]
        B -- false --> D["mkdir ./plugins"]
        C --> c1{"Loop done?"}
        c1 -- true --> c2["Loop all ready plugins"] 

        c1 -- false --> E{"if ./plugins/pluginA/main.py exist"}
        E -- true --> F["Mark ./plugins/pluginA ready"]
        F --> c1 

        c2 --> c3{"Loop done?"}
        c3 -- false -->  G["Look for main functions, register external modules, push valid main functions in to the list"]
        G --> c3
        c3 -- true --> H["Loop through list of ready main functions"]
        H --> h1{"Loop done?"}
        h1 -- false --> h2["Pass each main function in to a thread and start"]
        h2 --> h1
        h1 -- true --> J["All plugins are loaded"] 
```

## How to write your own plugin?
I've designed it so is super easy to do it. Every plugin will get load into a thread when WGDashboard starts. You just need to do the following step:

1. Create a new folder in `WGDashboard/src/plugins`, make sure your folder name **does not contain spaces**
2. In the folder create a Python file called `main.py`. This file will be the entry point of your plugin.
3. In your `main.py`, create a function called `main` that takes in **1** parameter, which is a dictionary containing all your WireGuard configurations.
    ```python
    # main.py
    def main(WireguardConfigurations: dict[str, object] = None):
       pass
    ```
    - This would allow you to read the latest data of your WireGuard configurations.

4. That's it, you can now do whatever you want, but make sure you understand what you're doing. You can look into the `plugin_template`

## Want to submit your plugin?

We always welcome users to contribute to our project! Please make a PR in this repo and we will review it :)