Model - 逻辑业务 如:登陆,load数据,
        如MLoginImpl 实现接口 MLoginInter:public void login(Object o,Listener listener);此方法里的Listener由Presenter调用该逻辑业务时实现该回调方法(或者说监听器)


View - activity,fragment,,  并且他们实现接口 ViewInterface
	ViewInterface 里的方法是用来给Presenter回调的 如:任务前的ui展现 和 任务完成后的ui展现 就是用的 ViewInterface 里的方法
        而 View 需要实现 ViewInterface 的各个方法.

Presenter - 实现 PresenterInterface 这里的方法保留
        Presenter 持有 多个 ViewInterface 和 多个 ModelInterface 
        Presenter里有各个逻辑业务方法 如Login 但是具体实现是调用Model的逻辑业务,但是它自己要主持一下任务前的UI展现,即回调View实现的ViewInterface接口,和实现调用Model后任务完成的回调Listener(或者说是监听器)
        而Model的各个逻辑业务方法 如 Login 又是实现事先定义好的 ModelInterface.



/////////////////////////////////////////////////////////////////////
原博客: http://blog.csdn.net/hrx3627/article/details/48031377
目录
MVP简介
MVP结构
MVP与MVC区别
实战演习
正文

1、MVP简介
相信大家对MVC都是比较熟悉了：M-Model-模型、V-View-视图、C-Controller-控制器，MVP作为MVC的演化版本，那么类似的MVP所对应的意义：M-Model-模型、V-View-视图、P-Presenter-表示器。从MVC和MVP两者结合来看，Controlller/Presenter在MVC/MVP中都起着逻辑控制处理的角色，起着控制各业务流程的作用。而MVP与MVC最不同的一点是M与V是不直接关联的也是就Model与View不存在直接关系，这两者之间间隔着的是Presenter层，其负责调控View与Model之间的间接交互，MVP的结构图如下所示，对于这个图理解即可而不必限于其中的条条框框，毕竟在不同的场景下多少会有些出入的。在Android中很重要的一点就是对UI的操作基本上需要异步进行也就是在MainThread中才能操作UI，所以对View与Model的切断分离是合理的。此外Presenter与View、Model的交互使用接口定义交互操作可以进一步达到松耦合也可以通过接口更加方便地进行单元测试。 

（引用该文章：http://zhengxiaopeng.com/2015/02/06/Android中的MVP/）

2、MVP结构
View View通常来说就是有Activity、Fragment实现的，View会包含一个或多个Presenter的引用来满足视图的业务逻辑。View和Presenter的交互是双向的，即View层可以调用Presenter的逻辑方法，Presenter也可以控制View的显示。 Presenter Presenter作为Model和View的桥梁，负责从Model拿到数据进行处理并返回给View。但Presenter和其他两层的沟通是通过接口协议进行的，所以每个Presenter中通常会包涵一个或多个接口协议。 Model 和MVC一样，作为数据仓库只负责对APP数据进行处理。 Android开发MVP模式实践中的示例将APP分为以下四层。

Entities:APP中的业务类。 Use Cases:负责从将Entities中的数据进行处理和包装。 Presenters:从Use Cases获取处理好的数据，然后根据需求逻辑为UI提供合适的数据。 UI:从Presenters获取处理好的最终数据，和用户进行直接交互。 这四层设计的原则是代码调用只能从外圆向内圆扩展，内圆不能干预也不需关心外圆的功能逻辑，这符合MVP的思想，Use Cases和Presenters将Entities和UI间隔分离，从而使Entities和UI只需关心自身逻辑，数据处理完全交给其他两层。 这里，有些同学可能会有疑问，说好的Presenters为什么会有Use Cases出来搅局？其实这也是我选择这个工程当做示例的目的，看了好多MVP文章，都在讲Presenter如何通过接口协议和其他两层进行交互，但大都忽略了Presenter层自身的构架，因为仅仅套用MVP模式，虽然在一定程度上降低View的耦合度，但因为Presenter既要处理数据，又要结合需求控制UI交互，所以很可能出现Presenter逻辑的冗余。后文的示例工程在Presenter和Model之间包装了Use Cases，将数据逻辑处理交给UseCases从而让Presenter更专心于UI交互。

（引用该文章：http://blog.csdn.net/guxiao1201/article/details/40147209）

3、MVP与MVC区别
在把原本MVC模式的代码修改为MVP模式后，总结这两个模式在实际使用过程中的不同点基本上总结为两点： 各个层之间通过接口协议进行沟通； View和Model不再进行直接交互；

（详细说明请参考MVC or MVP Pattern - Whats the difference?）

4、实战演习
模拟登录功能，实现MVP架构模式。下面是实战的具体步骤

NO1、新建VIew公共部分接口：

/**
 * Created by Bluesky on 2015/8/27.
 * MVP中V层的公共接口
 */

public interface IView {
public void showProgressPar();

public void hideProgressPar();

public void showError(Object o);
}
View继承公共IView接口

/**
 * Created by Bluesky on 2015/8/27.
 * 登录View接口
 */

public interface ILogin extends IView {
 public void showSuccess(Object o);
}
NO2、VIew的实现。也就是Activity实现ILogin接口：

/**
 *登录页面Activity
 */
public class MainActivity extends Activity implements ILogin {
private LoginPresenter mPresenter;
private User mUser;
private ProgressDialog mDialog;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    mPresenter = new LoginPresenter(this);
    mUser = new User();

    initVIew();
}

private void initVIew() {
    final EditText pwd = (EditText) findViewById(R.id.pwd);
    final EditText name = (EditText) findViewById(R.id.name);
    Button loginBtn= (Button) findViewById(R.id.login_btn);
    loginBtn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            mUser.setName(name.getText().toString());
            mUser.setPassword(pwd.getText().toString());
            mPresenter.login(mUser);
        }
    });


}

@Override
public boolean onCreateOptionsMenu(Menu menu) {
    // Inflate the menu; this adds items to the action bar if it is present.
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    // Handle action bar item clicks here. The action bar will
    // automatically handle clicks on the Home/Up button, so long
    // as you specify a parent activity in AndroidManifest.xml.
    int id = item.getItemId();

    //noinspection SimplifiableIfStatement
    if (id == R.id.action_settings) {
        return true;
    }

    return super.onOptionsItemSelected(item);
}


@Override
public void showSuccess(Object o) {
    User user= (User) o;
   Toast.makeText(this,"登录成功信息："+user.getName()+" /"+user.getPassword(),Toast.LENGTH_LONG).show();
}

@Override
public void showProgressPar() {
    mDialog = new ProgressDialog(MainActivity.this);
    mDialog.setMessage("正在加载...");
    mDialog.show();
}

@Override
public void hideProgressPar() {
    mDialog.hide();
}

@Override
public void showError(Object o) {
    Toast.makeText(this,"异常："+((Exception)o).getMessage(),Toast.LENGTH_LONG).show();

}
}
activity的xml布局：

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:tools="http://schemas.android.com/tools"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:orientation="vertical"
  android:paddingBottom="@dimen/activity_vertical_margin"
  android:paddingLeft="@dimen/activity_horizontal_margin"
  android:paddingRight="@dimen/activity_horizontal_margin"
  android:paddingTop="@dimen/activity_vertical_margin"
  tools:context=".MainActivity"
>

<TextView
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:text="@string/hello_world"/>

<EditText
android:id="@+id/name"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="请输入用户名"
/>

<EditText
android:id="@+id/pwd"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="请输入密码"
/>

<Button
android:id="@+id/login_btn"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="登录"/>


</LinearLayout>
No3、新建LoginPresenter。我们面向接口编程，所以，新建一个Presenter接口，在该Demo是没有什么方法，这是为了可扩展性考虑。 presenter接口

/**
 * Created by Bluesky on 2015/8/27.
 * MVP中P层
 */

public interface Presenter {

}
登录presenter实现presenter接口，在这里进行View和Model层桥梁连接，进行业务调度，起到指挥作用

/**
 * Created by Bluesky on 2015/8/27.
 */

public class LoginPresenter implements Presenter {
private ILogin mLoginView;
private ILoginBiz mLoginBiz;
private Handler mHandler = new Handler();

public LoginPresenter(ILogin mLoginView) {
    this.mLoginView = mLoginView;
    this.mLoginBiz = new LoginBizImpl();
}

/**
 * 登录
 *
 * @param o
 */
public void login(Object o) {
    mLoginView.showProgressPar();
    mLoginBiz.login(o, new Listener() {
        @Override
        public void complete() {
            mHandler.post(new Runnable() {
                @Override
                public void run() {
                    mLoginView.hideProgressPar();
                }
            });
        }

        @Override
        public void onSuccess(final Object o) {
            mHandler.post(new Runnable() {
                @Override
                public void run() {
                    mLoginView.showSuccess(o);
                }

            });
        }

        @Override
        public void onFailed(final Exception e) {
            mHandler.post(new Runnable() {
                @Override
                public void run() {
                    mLoginView.showError(e);
                }
            });

        }
    });
}
}
No4、Model层进行业务逻辑处理。新建model层接口，然后实现业务逻辑处理，做异步处理及子线程和主线程通讯。 model接口：

/**
 * Created by Bluesky on 2015/8/27.
 */
public interface ILoginBiz {
public void login(Object o,Listener listener);
}
model实现：

/**
 * Created by Bluesky on 2015/8/27.
 */
public class LoginBizImpl implements ILoginBiz {
@Override
public void login(Object o, final Listener listener) {
final User user = (User) o;
new Thread(new Runnable() {
@Override
public void run() {
try {
Thread.sleep(2 * 1000);
} catch (InterruptedException e) {
e.printStackTrace();
}
listener.complete();
if (user.getName().equals(user.getPassword())) {//成功
listener.onSuccess(user);
} else {//失败
listener.onFailed(new Exception("运行异常..."));
}
}
}).start();
}
}
实体类：

/**
 * Created by Bluesky on 2015/8/27.
 */

public class User implements Serializable {
private String name;
private String password;

public String getPassword() {
return password;
}

public void setPassword(String password) {
this.password = password;
}

public String getName() {
return name;

}

public void setName(String name) {
this.name = name;
}
}
回调接口：

/**
 * Created by Bluesky on 2015/8/27.
 */
public interface Listener {
public void complete();

public void onSuccess(Object o);

public void onFailed(Exception e);
}
源代码

https://github.com/hrx3627/MVPAndroidDemo

参考信息

http://www.imooc.com/wenda/detail/216700http://www.cnblogs.com/daizhj/archive/2009/04/30/1447035.HTMLhttp://blog.csdn.net/lmj623565791/article/details/46596109http://zhengxiaopeng.com/2015/02/06/Android中的MVP/http://blog.csdn.net/guxiao1201/article/details/40147209