#### Service的使用

* binder

1。创建binder类

```
public class MyBinder extends Binder {

    private MyService service;
    private OnListener listener;        

    public void msgFromService(String str) {
        listener.onTest(str);
    }

    interface OnListener{
        void onTest(String str);
    }

    public void activityToService(String str){
        service.msgFromAct(str);
    }

    public MyBinder(MyService service){
        this.service = service;
    }

    public void setListener(OnListener listener){
        this.listener = listener;
    }
}
```

2。创建Service类

```
public class MyService extends Service {


    private MyBinder mBinder = new MyBinder(this);

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        return mBinder;
    }


    public void msgFromService(String str){
        mBinder.msgFromService(str);
    }

    public void msgFromAct(String str){
        Log.e("MyService", "信息来自Activity "+ str);
    }
}
```

3。在Activity中用ServiceConnection连接

```
public class MyActivity extends AppCompatActivity{

    private MyBinder mBinder;

    private ServiceConnection connection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {
            mBinder = (MyBinder) service;

            mBinder.setListener(new MyBinder.OnListener() {
                @Override
                public void onTest(String str) {
                    Log.e("MyService", "来自Service " + str);
                }
            });

        }

        @Override
        public void onServiceDisconnected(ComponentName name) {

        }
    };


    public void test(){
        mBinder.activityToService("测试");

    }

}
```

总结

```
Service往Activity传数据

Activity往Service传数据
使用接口回调，在Activity中的binder设置监听等待Service传数据


```



