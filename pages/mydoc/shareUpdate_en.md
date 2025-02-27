---
title: Update Share
sidebar: mydoc_en_sidebar
permalink: shareUpdate_en.html
last_updated: 2019-03-20
folder: mydoc
layout: page_en
---

app send command to server to update the timer permissions given to sharee. This command will be used to change other permissions in future, such as uid,deviceName, etc.

- Request parameters：

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|apikey |Yes  |String |user apikey   |
|deviceid |Yes  |String | device id    |
|action     |Yes  |String | value is updateShare   |
|userAgent     |Yes  |String | value is app   |
|params     |Yes  |ShareParam |     |
|sequence     |Yes  |String | timestamp to millisecond    |

- ShareParam Definitions

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|uid |Yes  |String |user account,add +86 to accounts of users in China, user in other regions or countries need to select country or email   |
|deviceName |Yes  |String | device name   |
|permit     |No  |Int | sum of permission values,calculated by offset.permission values: 1:add new timers;2:edit timers;4:delete timers;8:enable timers    |
|note     |Yes  |String | share note of maximum 10 Chinese characters    |

```
1、permit computation rules：
   give permissions,such as to give user the permissions to add, edit,and enable timers.
   permit=1 | 2 | 8  result is 11

   add permissions on current basis
   permit= permit|xxx(specific permission values)

2、delete a certain permission,for example, permission value is 11, we want to delete the permission for 'edit'.
   now permit=11
   permit= permit ^ ( permit & 2)    2 is the permission value for 'edit timers，and result is 9 

3、delete multiple permissions, same example of current value 11, now we need to delete permissions for 'add timer'and 'edit timer'.
   First calculte the sum of permission values to be deleted
   delPermit= 1|2   result is 3
   Then calculate the permission value after deletion
   now permit=11
   permit= permit ^ ( permit & delPermit)

4、Check whether one permission exists or not.For example,current permission value is 11( permissions include 'add','edit', and 'enable').
   now permit=11
   Check permission for 'edit' 
   boolean isPermit=((permit & 2) == 2)   result is true
   Check permission for 'delete'
   boolean isPermit=((permit& 4) == 4)    result is false

5、Check multiple permissions,for instance, to delete multipl permissions.Need to check the sum of permission values first. 
   now permit=11
   Check if 'edit' and 'enable' permissions exist
   queryPermit = 2|8   result is 10
   boolean isPermit=((permit & queryPermit) == queryPermit)   result is true

   Check if 'edit' and 'delete' permissions exist
   queryPermit= 2|4   result is 6
   boolean isPermit=((permit & queryPermit) == queryPermit)   result is false

   Special Note for sharing Bridges：
   Note：For the 3 commands concerning share(share device, change share, and cancel share) of Bridges, pay attention to the following situations.
   1、When sending the 3 commands, app should check device ui first. If the device is a Zigbee bridge or similar devices, app should do the same operation(share device,change share, delete share) on sub devices.For example:
   Bridge deviceid: 1000001
   Sub Device deviceid: 1000002, 1000003

   User A share bridge 1000001 with user B, then the info of user B should be added to the shareUsers of not only the Bridge, but also sub devices 1000002 and 1000003.
   The permissions of sub devices should be the same as their bridge.

   If owner wants to set different permissions for a single sub device,he needs to select the sub device in app to change it separately, like setting up a regular device.
```

- Response parameters

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|error |Yes  |Int |error code   |
|result |No  |Int | 0:not sharer;1:user does not exist;2:update succeeded;3 update failed    |
|apikey     |No  |String | user apikey    |
|deviceid     |No  |String | device id    |
|sequence     |No  |String | timestamp to millisecond obtained from request parameters    |

```
error code
0: ok(operation succeeded)
400: Bad Request（wrong parameter）
401:Authorization failed
403:Forbidden（no permission）
406:User has logined on another device
500:Internal Server Error（Internal server error）
```


