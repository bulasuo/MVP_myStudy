Model - �߼�ҵ�� ��:��½,load����,
        ��MLoginImpl ʵ�ֽӿ� MLoginInter:public void login(Object o,Listener listener);�˷������Listener��Presenter���ø��߼�ҵ��ʱʵ�ָûص�����(����˵������)


View - activity,fragment,,  ��������ʵ�ֽӿ� ViewInterface
	ViewInterface ��ķ�����������Presenter�ص��� ��:����ǰ��uiչ�� �� ������ɺ��uiչ�� �����õ� ViewInterface ��ķ���
        �� View ��Ҫʵ�� ViewInterface �ĸ�������.

Presenter - ʵ�� PresenterInterface ����ķ�������
        Presenter ���� ��� ViewInterface �� ��� ModelInterface 
        Presenter���и����߼�ҵ�񷽷� ��Login ���Ǿ���ʵ���ǵ���Model���߼�ҵ��,�������Լ�Ҫ����һ������ǰ��UIչ��,���ص�Viewʵ�ֵ�ViewInterface�ӿ�,��ʵ�ֵ���Model��������ɵĻص�Listener(����˵�Ǽ�����)
        ��Model�ĸ����߼�ҵ�񷽷� �� Login ����ʵ�����ȶ���õ� ModelInterface.