When you start using a VS Code fork, you’ll quickly notice that it relies on OpenVSX for extensions. This is because Microsoft does not allow forks to use the official Visual Studio Marketplace out of the box. As a result, not all of your existing extensions will be available after migrating.

A common workaround is to manually install the missing extensions. However, as these forks have grown in popularity, Microsoft has removed direct download access from the Marketplace, making this approach increasingly impractical.

Fortunately, there’s a permanent solution that works across all editors to my knowledge—and the same approach can be adapted for other editors, even if they aren’t listed here.

## Cursor

Navigate to the following file (the exact location could differ, however it exists for sure so look around):

```
    Windows: C:\Users\<USERNAME>\AppData\Local\Programs\cursor\resources\app
    Mac: /Applications/Cursor.app/Contents/Resources/app
    Linux: ~/.local/share/cursor/resources/app/product.json
    Linux (remote): ~/.cursor-server/bin/<HASH>/product.json
```

Edit the JSON in this file to the following:

```json
    {
      "serviceUrl": "https://marketplace.visualstudio.com/_apis/public/gallery",
      "cacheUrl": "https://vscode.blob.core.windows.net/gallery/index",
      "itemUrl": "https://marketplace.visualstudio.com/items",
      "controlUrl": "https://az764295.vo.msecnd.net/extensions/marketplace.json",
      "recommendationsUrl": "https://az764295.vo.msecnd.net/extensions/workspaceRecommendations.json.gz"
    }
```

## Antigravity
This one is quite easy, go to `Antigravity Settings -> Editor` then change the following:
```
    Marketplace Item URL: https://marketplace.visualstudio.com/items
    Marketplace Gallery URL: https://marketplace.visualstudio.com/_apis/public/gallery
```

## Code Server
Depending on the version of code server you have (gitpod, coder) this may differ slightly. If the following doesnt work, try applying the Cursor method. However the following should work atleast for the coder version and also is easy to use with docker.

Set the following ENV variables, if you are using docker or some kind of containerization just set it the normal way to set environment variables in the container. If you are on a manual installation on your system, you will have to add this globally or add it into the startup script of cursor.

```
    EXTENSIONS_GALLERY={\"serviceUrl\": \"https://marketplace.visualstudio.com/_apis/public/gallery\", \"cacheUrl\": \"https://vscode.blob.core.windows.net/gallery/index\", \"itemUrl\": \"https://marketplace.visualstudio.com/items\", \"controlUrl\": \"https://az764295.vo.msecnd.net/extensions/marketplace.json\", \"recommendationsUrl\": \"https://az764295.vo.msecnd.net/extensions/workspaceRecommendations.json.gz\"}
```

## Other forks
Other forks, generally one of the above methods should work unless it changes something fundamentally about how extensions are processed. I would generally first recommend trying the Cursor method first since that should work in all cases.
