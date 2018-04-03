### Permissions

* [请求权限](#请求权限)

#### 请求权限

1. 先判断再请求

```
if(PackageManager.PERMISSION_GRANTED != ContextCompat.checkSelfPermission(context,Manifest.permission.)){
    ActivityCompat.requestPermissions(context, new String[]{model.permission.}, requestCode);
}
多个权限， 循环
```



