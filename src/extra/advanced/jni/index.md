# Jni

## Implement a new jni function

Add the following flags to the cmake command like
`cmake -DJNIVM_ENABLE_TRACE=ON -DJNIVM_USE_FAKE_JNI_CODEGEN=ON`, this
doesn't work if you have configured to use FakeJni ( `JNI_USE_JNIVM=OFF`
)

Edit this file
<https://github.com/minecraft-linux/mcpelauncher-client/blob/eb2465a1f59422b1cf11d14b9838eeb5d5c32237/src/jni/jni_support.cpp#L254>
and add

``` c++
vm.printStatistics();
```

- Running mcpelauncher-client now, will print almost every function call
  from the game to the fake java native interface.
- Closing the gamewindow now should log compileable stubs of the called
  functions **without class inherence**
- Put the class or method declaration into a new header file in
  <https://github.com/minecraft-linux/mcpelauncher-client/blob/eb2465a1f59422b1cf11d14b9838eeb5d5c32237/src/jni>.
- Put the stubs of the class / methods you want to implement into a new
  cpp file
- Put the class descriptor into
  <https://github.com/minecraft-linux/mcpelauncher-client/blob/eb2465a1f59422b1cf11d14b9838eeb5d5c32237/src/jni/jni_descriptors.cpp>
- Put `vm.registerClass<MyClass>()` into
  <https://github.com/minecraft-linux/mcpelauncher-client/blob/eb2465a1f59422b1cf11d14b9838eeb5d5c32237/src/jni/jni_support.cpp#L25>

Access FakeJni::JString ----------------------- call
`FakeJni::JString::asStdString()` to get a std::string - create a new
jni string with `std::make_shared<FakeJni::JString>("mycstr")`

## Register a native jni static function

To call native functions you have to register them first. Put

``` c++
registerNatives(BrowserLaunchActivity::getDescriptor(), {
    {"somefunction", "(JLjava/lang/String;)V"},
}, symResolver);
```

- `BrowserLaunchActivity` is the c++ class name of the jni class
- `"(JLjava/lang/String;)V"` is the jni descriptor of this native
  function describes the parameter and return value of the function, see
  the jdk jni documentation
- `"somefunction"` is the jni name of this function

into
<https://github.com/minecraft-linux/mcpelauncher-client/blob/eb2465a1f59422b1cf11d14b9838eeb5d5c32237/src/jni/jni_support.cpp#L91>

## Call a native jni instance function from an instance method

``` c++
auto method = getClass().getMethod("(JLjava/lang/String;)V", "somefunction");
FakeJni::LocalFrame frame;
method->invoke(frame.getJniEnv(), this, callback, frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr")));
```

- `frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr"))`
  creates a new jni reference for calling a native jni method
- `FakeJni::LocalFrame frame;` reads the current attached fake jvm for
  this thread and creates a new jni reference frame, it's destructor
  releases all local references of this frame. Call the contructor with
  a vm object to create a frame on detached threads.
- `"(JLjava/lang/String;)V"` is the jni descriptor of this native
  function describes the parameter and return value of the function, see
  the jdk jni documentation
- `"somefunction"` is the jni name of this function

## Call a native jni static function from an instance method

``` c++
auto method = getClass().getMethod("(JLjava/lang/String;)V", "somefunction");
FakeJni::LocalFrame frame;
method->invoke(frame.getJniEnv(), &getClass(), callback, frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr")));
```

- `frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr"))`
  creates a new jni reference for calling a native jni method
- `FakeJni::LocalFrame frame;` reads the current attached fake jvm for
  this thread and creates a new jni reference frame, it's destructor
  releases all local references of this frame. Call the contructor with
  a vm object to create a frame on detached threads.
- `"(JLjava/lang/String;)V"` is the jni descriptor of this native
  function describes the parameter and return value of the function, see
  the jdk jni documentation
- `"somefunction"` is the jni name of this function

## Call an arbitary native jni static function from an instance method

``` c++
auto method = BrowserLaunchActivity::getDescriptor()->getMethod("(JLjava/lang/String;)V", "somefunction");
FakeJni::LocalFrame frame;
method->invoke(frame.getJniEnv(), BrowserLaunchActivity::getDescriptor().get(), callback, frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr")));
```

- `frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr"))`
  creates a new jni reference for calling a native jni method
- `FakeJni::LocalFrame frame;` reads the current attached fake jvm for
  this thread and creates a new jni reference frame, it's destructor
  releases all local references of this frame. Call the contructor with
  a vm object to create a frame on detached threads.
- `"(JLjava/lang/String;)V"` is the jni descriptor of this native
  function describes the parameter and return value of the function, see
  the jdk jni documentation
- `"somefunction"` is the jni name of this function

## Call an arbitary native jni static function from anywhere

``` c++
// A reference to the jvm, you might have to manually pass them to your function or class
Baron::Jvm vm;
//...
FakeJni::LocalFrame frame(&vm);
auto method = BrowserLaunchActivity::getDescriptor()->getMethod("(JLjava/lang/String;)V", "somefunction");
method->invoke(frame.getJniEnv(), BrowserLaunchActivity::getDescriptor().get(), callback, frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr")));
```

- `frame.getJniEnv().createLocalReference(std::make_shared<FakeJni::JString>("mystr"))`
  creates a new jni reference for calling a native jni method
- `FakeJni::LocalFrame frame;` reads the current attached fake jvm for
  this thread and creates a new jni reference frame, it's destructor
  releases all local references of this frame. Call the contructor with
  a vm object to create a frame on detached threads.
- `"(JLjava/lang/String;)V"` is the jni descriptor of this native
  function describes the parameter and return value of the function, see
  the jdk jni documentation
- `"somefunction"` is the jni name of this function

## Create a global jni reference of a c++ object

``` c++
// A reference to the jvm, you might have to manually pass them to your function or class
Baron::Jvm vm;
//...
auto activity = std::make_shared<MainActivity>();
auto activityRef = vm.createGlobalReference(activity);
```
