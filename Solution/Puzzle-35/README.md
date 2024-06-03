# Blazor Puzzle #35

## Encrypt This!

YouTube Video: https://youtu.be/LtBlbjcrIFI

Blazor Puzzle Home Page: https://blazorpuzzle.com

### The Challenge:

This is a Global Server Blazor Web App that writes a string to local storage. The string is saved on the client and sent down in clear text. How can we encrypt the string to protect it from prying eyes?

### The Solution:

The solution is to use `ProtectedLocalStorage`, which encrypts local storage data, but only works with Blazor Server apps.

At the top of *Home.razzor*: we can inject:

```c#
@using Microsoft.AspNetCore.Components.Server.ProtectedBrowserStorage
@inject ProtectedLocalStorage ProtectedLocalStorage
```

Now, we just have to use it instead of calling to JavaScript:

```c#
async Task SaveData()
{
    //await jSRuntime.InvokeVoidAsync("SaveToLocalStorage", Key, Data);
    await ProtectedLocalStorage.SetAsync(Key, Data);
}

async Task LoadData()
{
    //Data = await jSRuntime.InvokeAsync<string>("GetFromLocalStorage", Key);
    Data = (await ProtectedLocalStorage.GetAsync<string>(Key)).Value;
}
```

Boom!

Oh yeah, don't ever save credit cards like this. :)
