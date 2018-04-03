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
                if(ActivityCompat.shouldShowRequestPermissionRationale(mContext, permissions[0])){
                    new 对话框{
                        applyPermissions();
                    }
                }else{
                // 到这里就表示已经是第3+次请求，而且此时用户已经永久拒绝了，这个时候，我们引导用户到应用权限页面，让用户自己手动打开
                    new 对话框{
                        openApplicationSettings(mRequestCode)
                    }
                }

            }
            
            if(isAllRequestedPermissionGranted()){
                请求成功，执行用户动作
            }else{
                applyPermissions()
            }


        break;
        ...
    }
}

//打开系统设置
private boolean openApplicationSettings(int requestCode) {
    try {
        Intent intent =
        	new Intent(Settings.ACTION_APPLICATION_DETAILS_SETTINGS, Uri.parse("package:" + mActivity.getPackageName()));
        intent.addCategory(Intent.CATEGORY_DEFAULT);
        
        // Android L 之后Activity的启动模式发生了一些变化
        // 如果用了下面的 Intent.FLAG_ACTIVITY_NEW_TASK ，并且是 startActivityForResult
        // 那么会在打开新的activity的时候就会立即回调 onActivityResult
        // intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        mActivity.startActivityForResult(intent, requestCode);
        return true;
    } catch (Throwable e) {
        Log.e(TAG, "", e);
    }
    return false;
		
}

//判断是否所有的权限都被授权了

public boolean isAllRequestedPermissionGranted() {
	for (mPermission : mPermissions) {
		if (PackageManager.PERMISSION_GRANTED != ContextCompat.checkSelfPermission(mActivity, mPermission)) {
			return false;
		}
	}
	return true;
}
```

#### 自定义权限

待

