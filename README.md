# react-native-android-templates
File &amp; live templates for React Native Android native module development

## File Templates
### Native Java Module
```
import com.facebook.react.bridge.ReactApplicationContext;
#if (${Events} == true)import com.facebook.react.bridge.ReactContext;#end
import com.facebook.react.bridge.ReactContextBaseJavaModule;
#if (${Events} == true)import com.facebook.react.bridge.WritableMap;#end
#if (${Events} == true)import com.facebook.react.modules.core.DeviceEventManagerModule;#end

#if (${Constants} == true)import java.util.HashMap;#end
#if (${Constants} == true)import java.util.Map;#end

#if (${Events} == true || ${Constants} == true)import javax.annotation.Nullable;#end

public class ${NAME} extends ReactContextBaseJavaModule {

    private static final String MODULE_NAME = "${NAME}";
#if (${Constants} == true)
    private static final Map<String, Object> CONSTANTS;

    static {
        final Map<String, Object> constants = new HashMap<>();
        CONSTANTS = constants;
    }
 #end
    
    // TODO Register module in ReactPackage
    public ${NAME}(ReactApplicationContext reactContext) {
        super(reactContext);
    }

    @Override
    public String getName() {
        return MODULE_NAME;
    }
#if (${Constants} == true)

    @Nullable
    @Override
    public Map<String, Object> getConstants() {
        return CONSTANTS;
    }
#end
#if (${Events} == true)

private void sendEvent(ReactContext reactContext,
                           String eventName,
                           @Nullable WritableMap params) {
        reactContext
                .getJSModule(DeviceEventManagerModule.RCTDeviceEventEmitter.class)
                .emit(eventName, params);
    }
#end
}
```

## Live Templates
### React Method (with Promise parameter) - `rm`
```
@ReactMethod
public void $NAME$(Promise promise) {
    $END$
}
```
### Resolve Promise with map - `resmap`
```
WritableMap map = Arguments.createMap();
promise.resolve(map);
```
### Resolve Promise with array - `resarr`
```
WritableArray array = Arguments.createArray();
promise.resolve(array);
```
### Create helper method to send React Native events - `rne`
```
private void sendEvent(ReactContext reactContext,
                           String eventName,
                           @Nullable WritableMap params) {
    reactContext
            .getJSModule(DeviceEventManagerModule.RCTDeviceEventEmitter.class)
            .emit(eventName, params);
}
```

### Create ActivityEventListener - `ael`
```
private static final int REQUEST_$REQUEST_NAME$ = 1;
private static final int ERROR_CANCELLED = -1;

private final ActivityEventListener $FIELD_NAME$ = new BaseActivityEventListener(){
    // TODO Register in constructor (reactContext.addActivityEventListener($FIELD_NAME$))
    @Override
    public void onActivityResult(Activity activity, int requestCode, int resultCode, Intent intent) {
        if (requestCode == REQUEST_CODE) {
            if ($PROMISE_FIELD$ != null) {
                if (resultCode == Activity.RESULT_CANCELED) {
                    $PROMISE_FIELD$.reject(ERROR_CANCELLED);
                } else if (resultCode == Activity.RESULT_OK) {
                    $END$
                }
            }
        }
    }
};
```

### Create React method to startActivityForResult - `sar`
```
@ReactMethod
public void $NAME$(Promise promise) {
    final Activity activity = getCurrentActivity();
     
    if (activity == null) {
        promise.reject(ERROR_NO_ACTIVITY, "Activity doesn't exist");
        return;
    }

    this.$NAME$Promise = promise;

    final Intent intent = new Intent($ACTIVITY$.class);
    activity.startActivityForResult(intent, $UPPER_NAME$_REQUEST_CODE);
}
```
