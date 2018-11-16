#Android 基础

###深入理解application

1. Application是什么
	
	1. 官网描述
	
	Base class for those who need to maintain global application state. You can provide your own implementation by specifying its name in your AndroidManifest.xml's <application> tag, which will cause that class to be instantiated for you when the process for your application/package is created.
	
	Application类是为了那些需要保存全局变量设计的基本类，你可以在AndroidManifest.xml的标签中进行自己的定义实现，这样的结果是：当你的application或者包被建立的时候，这个类就会被实例化。

	Note: There is normally no need to subclass Application. In most situations, static singletons can provide the same functionality in a more modular way. If your singleton needs a global context (for example to register broadcast receivers), include Context.getApplicationContext() as a Context argument when invoking your singleton’s getInstance() method.

	对应译文：正常情况下来说，创建一个application子类并不是必须的，在很多情况下，单例模式在更多模块化的方式下能起到相同的效果，如果单例需要全局context，可以利用Context.getApplicationContext()拿到Context对象从而引用单例的getInstance()方法。

	1. 理解
		1. Android系统会为会为每一个程序运行时创建一个application，且有且只有一个
		2. application的生命周期是整个程序中最长的，它的生命周期就等于这个程序的生命周期，因为他是全局单例的，在activity，service中获取到的对象都是同一个，所以通过application来进行一些数据的传递，数据的共享等数据缓存等；
		3. 启动application的时候系统会创建一个PID，即进程ID，所有的Acticity都会在此进行上运行，那么我们在Application创建的时候初始化全局变量，同一个应用的所有Activity都可以获取到全局变量的值，某一个Activity

	2. application的生命周期
		1. onCreate（） 这个就是应用初始化调用的方法，主要做一些配置之类的工作，不可以做延时工作不然会增加应用的启动时间；
		2. onLowMemory() 当后台程序已经终止且资源还比较紧张的时候就会回调这个方法，一般的应用程序会在这个方法中回调这个来释放一些不必要的资源来应对前台应用程序内存不够的情况
		3. onTrimMemory（）
			1. 通知 应用程序 当前内存使用情况（以内存级别进行识别）
			2. 根据当前内存使用情况进行自身的内存资源的不同程度释放，以避免被系统直接杀掉 & 优化应用程序的性能体验
		4. onConfigurationChanged（）监听 应用程序 配置信息的改变，如屏幕旋转等
		5. registerActivityLifecycleCallbacks（） & unregisterActivityLifecycleCallbacks（）注册 / 注销对 应用程序内 所有Activity的生命周期监听，当应用程序内 Activity生命周期发生变化时就会调用




			    registerActivityLifecycleCallbacks(new ActivityLifecycleCallbacks() {
	            @Override
	            public void onActivityCreated(Activity activity, Bundle savedInstanceState) {
	                Log.d(TAG,"onActivityCreated: " + activity.getLocalClassName());
	            }
	
	            @Override
	            public void onActivityStarted(Activity activity) {
	                Log.d(TAG,"onActivityStarted: " + activity.getLocalClassName());
	            }
	
	            @Override
	            public void onActivityResumed(Activity activity) {
	                Log.d(TAG,"onActivityResumed: " + activity.getLocalClassName());
	            }
	
	            @Override
	            public void onActivityPaused(Activity activity) {
	                Log.d(TAG,"onActivityPaused: " + activity.getLocalClassName());
	            }
	
	            @Override
	            public void onActivityStopped(Activity activity) {
	                Log.d(TAG, "onActivityStopped: " + activity.getLocalClassName());
	            }
	
	            @Override
	            public void onActivitySaveInstanceState(Activity activity, Bundle outState) {
	            }
	
	            @Override
	            public void onActivityDestroyed(Activity activity) {
	                Log.d(TAG,"onActivityDestroyed: " + activity.getLocalClassName());
	     	       }
	     		   });


		6. onTerminate（）应用程序结束时调用，但该方法只用于Android仿真机测试，在Android产品机是不会调用的


###应用场景
1. 从Application类的方法可以看出，Application类的应用场景有：
	1. 初始化应用级别的资源，如全局对象，环境配置变量等
	2. 数据共享，数据缓存，如设置全局共享变量，方法等
	3. 获取应用程序当前的内存使用情况，及时的释放资源，从而避免被系统杀死；
	4. 监听应用程序配置信息的改变，如屏幕旋转等
	5. 监听应用程序内，所有的Actvity的生命周期