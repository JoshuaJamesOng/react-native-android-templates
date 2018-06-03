# react-native-android-templates
File &amp; live templates for React Native Android native module development

## File Templates
### Native Java Module
```
import com.facebook.react.bridge.ReactApplicationContext;
import com.facebook.react.bridge.ReactContextBaseJavaModule;

import java.util.HashMap;
import java.util.Map;

import javax.annotation.Nullable;

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
