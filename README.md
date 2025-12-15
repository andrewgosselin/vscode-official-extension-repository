When you start using any vscode fork, you will quickly realize that it uses OpenVSX for its extension repository and that not all of your extensions get migrated over. A temporary fix is to just manually install the extension, however since the popularity of some of these forks it seems microsoft removed the direct download from the marketplace, making this hard. So here is the permanent solution for all of the editors to my knowledge (you can apply it in a similar fashion to all editors even not listed).

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
