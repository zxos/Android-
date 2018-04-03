### Permissions

* [请求权限](#请求权限)
* [自定义权限](#自定义权限)

#### 请求权限

1、先判断再请求

```
public void applyPermissions(){
    如果多个权限， 循环
    if(PackageManager.PERMISSION_GRANTED != ContextCompat.checkSelfPermission(mContext,mPermission)){
        ActivityCompat.requestPermissions(mContext, new String[]{mPermission}, mRequestCode);
    }
}
```

2、根据请求结果做处理

```
@Override
public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults){
    switch(requestCode){
        case mRequestCode:

            if(PackageManager.PERMISSION_GRANTED != grantResults[0]){
                
                //以前请求过这个权限，但是用户拒接了
                // 因此这里需要给用户解释一下我们为什么需要这个权限，否则用户可能会永久不在激活这个申请
                if(ActivityCompat.shouldShowRequestPermissionRationale(mContext))
                
            }
            
            
        break;
        ...
    }
}
```



#### 自定义权限

待





