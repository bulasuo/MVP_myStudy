Model - �߼�ҵ�� ��:��½,load����,
        ��MLoginImpl ʵ�ֽӿ� MLoginInter:public void login(Object o,Listener listener);�˷������Listener��Presenter���ø��߼�ҵ��ʱʵ�ָûص�����(����˵������)


View - activity,fragment,,  ��������ʵ�ֽӿ� ViewInterface
	ViewInterface ��ķ�����������Presenter�ص��� ��:����ǰ��uiչ�� �� ������ɺ��uiչ�� �����õ� ViewInterface ��ķ���
        �� View ��Ҫʵ�� ViewInterface �ĸ�������.

Presenter - ʵ�� PresenterInterface ����ķ�������
        Presenter ���� ��� ViewInterface �� ��� ModelInterface 
        Presenter���и����߼�ҵ�񷽷� ��Login ���Ǿ���ʵ���ǵ���Model���߼�ҵ��,�������Լ�Ҫ����һ������ǰ��UIչ��,���ص�Viewʵ�ֵ�ViewInterface�ӿ�,��ʵ�ֵ���Model��������ɵĻص�Listener(����˵�Ǽ�����)
        ��Model�ĸ����߼�ҵ�񷽷� �� Login ����ʵ�����ȶ���õ� ModelInterface.



/////////////////////////////////////////////////////////////////////
ԭ����: http://blog.csdn.net/hrx3627/article/details/48031377
Ŀ¼
MVP���
MVP�ṹ
MVP��MVC����
ʵս��ϰ
����

1��MVP���
���Ŵ�Ҷ�MVC���ǱȽ���Ϥ�ˣ�M-Model-ģ�͡�V-View-��ͼ��C-Controller-��������MVP��ΪMVC���ݻ��汾����ô���Ƶ�MVP����Ӧ�����壺M-Model-ģ�͡�V-View-��ͼ��P-Presenter-��ʾ������MVC��MVP���߽��������Controlller/Presenter��MVC/MVP�ж������߼����ƴ���Ľ�ɫ�����ſ��Ƹ�ҵ�����̵����á���MVP��MVC�ͬ��һ����M��V�ǲ�ֱ�ӹ�����Ҳ�Ǿ�Model��View������ֱ�ӹ�ϵ��������֮�����ŵ���Presenter�㣬�为�����View��Model֮��ļ�ӽ�����MVP�Ľṹͼ������ʾ���������ͼ��⼴�ɶ������������е�������򣬱Ͼ��ڲ�ͬ�ĳ����¶��ٻ���Щ����ġ���Android�к���Ҫ��һ����Ƕ�UI�Ĳ�����������Ҫ�첽����Ҳ������MainThread�в��ܲ���UI�����Զ�View��Model���жϷ����Ǻ���ġ�����Presenter��View��Model�Ľ���ʹ�ýӿڶ��彻���������Խ�һ���ﵽ�����Ҳ����ͨ���ӿڸ��ӷ���ؽ��е�Ԫ���ԡ� 

�����ø����£�http://zhengxiaopeng.com/2015/02/06/Android�е�MVP/��

2��MVP�ṹ
View Viewͨ����˵������Activity��Fragmentʵ�ֵģ�View�����һ������Presenter��������������ͼ��ҵ���߼���View��Presenter�Ľ�����˫��ģ���View����Ե���Presenter���߼�������PresenterҲ���Կ���View����ʾ�� Presenter Presenter��ΪModel��View�������������Model�õ����ݽ��д������ظ�View����Presenter����������Ĺ�ͨ��ͨ���ӿ�Э����еģ�����ÿ��Presenter��ͨ�������һ�������ӿ�Э�顣 Model ��MVCһ������Ϊ���ݲֿ�ֻ�����APP���ݽ��д��� Android����MVPģʽʵ���е�ʾ����APP��Ϊ�����Ĳ㡣

Entities:APP�е�ҵ���ࡣ Use Cases:����ӽ�Entities�е����ݽ��д���Ͱ�װ�� Presenters:��Use Cases��ȡ����õ����ݣ�Ȼ����������߼�ΪUI�ṩ���ʵ����ݡ� UI:��Presenters��ȡ����õ��������ݣ����û�����ֱ�ӽ����� ���Ĳ���Ƶ�ԭ���Ǵ������ֻ�ܴ���Բ����Բ��չ����Բ���ܸ�ԤҲ���������Բ�Ĺ����߼��������MVP��˼�룬Use Cases��Presenters��Entities��UI������룬�Ӷ�ʹEntities��UIֻ����������߼������ݴ�����ȫ�����������㡣 �����Щͬѧ���ܻ������ʣ�˵�õ�PresentersΪʲô����Use Cases�������֣���ʵ��Ҳ����ѡ��������̵���ʾ����Ŀ�ģ����˺ö�MVP���£����ڽ�Presenter���ͨ���ӿ�Э�������������н��������󶼺�����Presenter������Ĺ��ܣ���Ϊ��������MVPģʽ����Ȼ��һ���̶��Ͻ���View����϶ȣ�����ΪPresenter��Ҫ�������ݣ���Ҫ����������UI���������Ժܿ��ܳ���Presenter�߼������ࡣ���ĵ�ʾ��������Presenter��Model֮���װ��Use Cases���������߼�������UseCases�Ӷ���Presenter��ר����UI������

�����ø����£�http://blog.csdn.net/guxiao1201/article/details/40147209��

3��MVP��MVC����
�ڰ�ԭ��MVCģʽ�Ĵ����޸�ΪMVPģʽ���ܽ�������ģʽ��ʵ��ʹ�ù����еĲ�ͬ��������ܽ�Ϊ���㣺 ������֮��ͨ���ӿ�Э����й�ͨ�� View��Model���ٽ���ֱ�ӽ�����

����ϸ˵����ο�MVC or MVP Pattern - Whats the difference?��

4��ʵս��ϰ
ģ���¼���ܣ�ʵ��MVP�ܹ�ģʽ��������ʵս�ľ��岽��

NO1���½�VIew�������ֽӿڣ�

/**
 * Created by Bluesky on 2015/8/27.
 * MVP��V��Ĺ����ӿ�
 */

public interface IView {
public void showProgressPar();

public void hideProgressPar();

public void showError(Object o);
}
View�̳й���IView�ӿ�

/**
 * Created by Bluesky on 2015/8/27.
 * ��¼View�ӿ�
 */

public interface ILogin extends IView {
 public void showSuccess(Object o);
}
NO2��VIew��ʵ�֡�Ҳ����Activityʵ��ILogin�ӿڣ�

/**
 *��¼ҳ��Activity
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
   Toast.makeText(this,"��¼�ɹ���Ϣ��"+user.getName()+" /"+user.getPassword(),Toast.LENGTH_LONG).show();
}

@Override
public void showProgressPar() {
    mDialog = new ProgressDialog(MainActivity.this);
    mDialog.setMessage("���ڼ���...");
    mDialog.show();
}

@Override
public void hideProgressPar() {
    mDialog.hide();
}

@Override
public void showError(Object o) {
    Toast.makeText(this,"�쳣��"+((Exception)o).getMessage(),Toast.LENGTH_LONG).show();

}
}
activity��xml���֣�

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
android:hint="�������û���"
/>

<EditText
android:id="@+id/pwd"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="����������"
/>

<Button
android:id="@+id/login_btn"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="��¼"/>


</LinearLayout>
No3���½�LoginPresenter����������ӿڱ�̣����ԣ��½�һ��Presenter�ӿڣ��ڸ�Demo��û��ʲô����������Ϊ�˿���չ�Կ��ǡ� presenter�ӿ�

/**
 * Created by Bluesky on 2015/8/27.
 * MVP��P��
 */

public interface Presenter {

}
��¼presenterʵ��presenter�ӿڣ����������View��Model���������ӣ�����ҵ����ȣ���ָ������

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
 * ��¼
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
No4��Model�����ҵ���߼������½�model��ӿڣ�Ȼ��ʵ��ҵ���߼��������첽�������̺߳����߳�ͨѶ�� model�ӿڣ�

/**
 * Created by Bluesky on 2015/8/27.
 */
public interface ILoginBiz {
public void login(Object o,Listener listener);
}
modelʵ�֣�

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
if (user.getName().equals(user.getPassword())) {//�ɹ�
listener.onSuccess(user);
} else {//ʧ��
listener.onFailed(new Exception("�����쳣..."));
}
}
}).start();
}
}
ʵ���ࣺ

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
�ص��ӿڣ�

/**
 * Created by Bluesky on 2015/8/27.
 */
public interface Listener {
public void complete();

public void onSuccess(Object o);

public void onFailed(Exception e);
}
Դ����

https://github.com/hrx3627/MVPAndroidDemo

�ο���Ϣ

http://www.imooc.com/wenda/detail/216700http://www.cnblogs.com/daizhj/archive/2009/04/30/1447035.HTMLhttp://blog.csdn.net/lmj623565791/article/details/46596109http://zhengxiaopeng.com/2015/02/06/Android�е�MVP/http://blog.csdn.net/guxiao1201/article/details/40147209