```js
 async: {
     enable: true,
     type: 'get',
     url: function(treeId, treeNode) {
         // treeNode 不存在时表示需要加载根节点下的数据
         var paperDirectoryId = treeNode ? treeNode.paperDirectoryId : 0;
         return Urls.REST_PAPER_SUBDIRECTORIES.format({paperDirectoryId: paperDirectoryId});
     },
     dataFilter: function(treeId, parentNode, result) {
         if (result.success) {
             var directories = result.data;
             for (var i = 0; i < directories.length; i++) {
                 directories[i].isParent = true;
             }
             return directories;
         }
 
         return null;
     }
 },
```



