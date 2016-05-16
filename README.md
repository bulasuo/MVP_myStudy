Model - 逻辑业务 如:登陆,load数据,
        如MLoginImpl 实现接口 MLoginInter:public void login(Object o,Listener listener);此方法里的Listener由Presenter调用该逻辑业务时实现该回调方法(或者说监听器)


View - activity,fragment,,  并且他们实现接口 ViewInterface
	ViewInterface 里的方法是用来给Presenter回调的 如:任务前的ui展现 和 任务完成后的ui展现 就是用的 ViewInterface 里的方法
        而 View 需要实现 ViewInterface 的各个方法.

Presenter - 实现 PresenterInterface 这里的方法保留
        Presenter 持有 多个 ViewInterface 和 多个 ModelInterface 
        Presenter里有各个逻辑业务方法 如Login 但是具体实现是调用Model的逻辑业务,但是它自己要主持一下任务前的UI展现,即回调View实现的ViewInterface接口,和实现调用Model后任务完成的回调Listener(或者说是监听器)
        而Model的各个逻辑业务方法 如 Login 又是实现事先定义好的 ModelInterface.