

main函数：

```C++
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    Widget w;
    w.show();
    return a.exec();
}
```

`QApplication a(argc, argv);`  应用程序对象，有且只有一个。

`Widget w;` 实例化窗口对象。

`w.show();` 调用show()函数，显示窗口。

`return a.exec();` 让应用程序对象进入消息循环机制中，代码阻塞当前行，等待下一步信息。



窗口常用设置

```C++
//  设置窗口标题
this->setWindowTitle("test");
//  重新指定大小   宽、高
this->resize(600, 400);

//  设置窗口大小固定，用户不可调整
this->setFixedSize(600, 400);
//  单独设置宽/高固定，不可修改，但是高/宽仍然可以修改
this->setFixedWidth(500);
this->setFixedHeight(500);
```





按钮控件API

```c++
//  头文件
#include <QPushButton>

//  创建在堆区
QPushButton * btn = new QPushButton(this);
//  this 代表  btn->setParent(this)

//  设置文本
btn->setText("class is over");
//  移动
btn->move(275, 150);
//  重新指定大小
btn->resize(100, 30);
```





使用debug打印结果

```C++
//  在应用程序输出打印结果
#include <QDebug>

qDebug() << "widget unconstruction";

//  QT中的字符串类型 默认为 QString，qDebug()输出QString会自带一个“”
//  类型转换  QString -> char*
//  name -> QString
name = name.toUtf8().data();
```





自定义信号/槽，及其重载时的处理方法

--  信号  --

1、自定义信号写在`.h`文件的`signals`下

2、必须返回void()

3、只需要声明，不需要实现

4、可以有参数，可以发生重载

--  槽  --

1、自定义槽写在`.h`文件的`public slots:`下，也可以直接写在`public:`下

2、必须返回void()

3、需要声明，也需要在`.cpp`文件中实现

4、可以有参数，可以发生重载



自定义信号重载时的处理方法

```C++
//  信号  声明    .h
singals:
    void signal1();
    void signal1(QString val);

//  槽   声明    .h
public slots:
	void slot1();
	void slot1(QString val)
//  槽   实现    .cpp
void CLASS::slot1(){
    qDebug() << "无参数";
}
void CLASS::slot1(QString val){
    qDebug() << "有参数" << val.toUtf8().data();
}

////////////////////////////////////////////////

//  发送者 Sender   接受者 Recipient
//  .h
#include "sender.h"
#include "recipient.h"

private:
	Sender * s;
	Recipient * r;
//  .cpp
this -> s = new Sender(this);
this -> r = new Recipient(this);

//  直接使用
//  connect(s, &Sender::signal1, r, &Recipient::slot1);
//  会发生错误，需要指定:

void(Sender::*senderSignal)(QString) = &Sender::signal1;
void(Recipient::*recipientSignal)(QString) = &Recipient::slot1;
connect(s, senderSignal, r, recipientSignal)

```



```C++
//  信号可以连接另一个信号
//  一个信号可以连接多个槽函数
//  多个信号可以连接同一个槽函数
//  信号和槽函数 的参数  必须一一对应
//  信号的参数个数可以多于槽函数的参数个数，多余部分被槽函数丢弃
//      但是前面的部分，参数类型必须一一对应
```



使用 lambda表达式控制

```
QPushButton * btnClose = new QPushButton(this);
connect(btnClose, &QPushButton::clicked, this, [this](){this->close();});
```







QMAINWindow

```c++
//  1 Window Title      窗口标题
//  2 Menu Bar          菜单栏      只能有一个
//  3 Tool Bar Area     工具栏
//  4 Status Bar        状态栏      只能有一个
//  5 Dock Widget Area  锚接部件（浮动窗口）
//  6 Central Widget    中心部件     只能有一个
```





1 窗口标题

```C++
this->setWindowTitle("我的窗口");
```



2 菜单栏   只能有一个

```C++
//  初始化
QMenuBar* bar = menuBar();
setMenuBar(bar);

//  主要操作
QMenu* fileMenu = bar->addMenu("文件");
QMenu* editMenu = bar->addMenu("编辑");

QAction* newAct =  fileMenu->addAction("新建");
QAction* openAct = fileMenu->addAction("打开");
//  注：QAction 的变量可以被 addAction()接受
fileMenu->addSeparator();
fileMenu->addAction("保存");
```



3 工具栏

```C++
//  初始化，初始停靠在左侧
QToolBar* toolBar = new QToolBar(this);
addToolBar(Qt::LeftToolBarArea, toolBar);

//  仅允许在左/右贴靠，不允许上/下贴靠
toolBar->setAllowedAreas(Qt::LeftToolBarArea | Qt::RightToolBarArea);
//  禁止浮动
toolBar->setFloatable(false);

//  在工具栏上添加一个按钮
QPushButton* btn = new QPushButton("click this", this);
toolBar->addWidget(btn);
```



4 状态栏   只能有一个

```C++
//  初始化
QStatusBar* stBar = statusBar();
setStatusBar(stBar);

QLabel* lab1 = new QLabel("左下角的提示信息", this);
stBar->addWidget(lab1);

QLabel* lab2 = new QLabel("右下角的提示信息", this);
stBar->addPermanentWidget(lab2);
```



5 锚接部件（浮动窗口）

```C++
//  初始化，设置在中心窗口(Central Widget)底部浮动
QDockWidget* dockWidget = new QDockWidget("浮动窗口", this);
addDockWidget(Qt::BottomDockWidgetArea, dockWidget);
```



6 中心部件   只能有一个

```C++
QTextEdit* edit = new QTextEdit("中心窗口", this);
setCentralWidget(edit);
```



```C++
助记

//  菜单栏和状态栏都只能有一个，创建时分别是：
QMenuBar* bar = menuBar();   setMenuBar(bar);
QStatusBar* stBar = statusBar();   setStatusBar(stBar);
//  这两个不需要new，起名时需要注意：习惯上 一个是bar，一个是stBar
//  不需要new的不带Q，需要new的有Q


//  中心部件也只能有一个，创建时是：
QTextEdit* edit = new QTextEdit("中心窗口", this);   setCentralWidget(edit);
//  这个需要new，起名时直接叫edit即可


//  工具栏和锚接部件可以有多个，创建时分别是
QToolBar* toolBar = new QToolBar(this);
addToolBar(Qt::LeftToolBarArea, toolBar);
QDockWidget* dockWidget = new QDockWidget("浮动窗口", this);
addDockWidget(Qt::BottomDockWidgetArea, dockWidget);
//  这两个起名时可以写全，分别是toolBar和dockWidget
```





对话框分类：

模态对话框：弹出时不可对其他窗口操作

非模态对话框：弹出时可以对其他窗口操作

```C++
//  已通过ui建立一个名字叫actionnew的对象

//  模态对话框
connect(ui.actionnew, &QAction::triggered, [this]() {
    //  不用开在堆区
    QDialog dlg(this);
    dlg.resize(200, 100);
    //  会阻塞当前代码，不再向后运行，因此前面的局部变量不会被释放
    dlg.exec();
    qDebug() << "模态对话框";

});

connect(ui.actionnew, &QAction::triggered, [this]() {
    //  建立在堆区
    QDialog* dlg2 = new QDialog(this);
    dlg2->resize(200, 100);
  	//  关闭时释放堆区
    dlg2->setAttribute(Qt::WA_DeleteOnClose);
    //  show不会阻塞当前代码
    dlg2->show();
    qDebug() << "非模态对话框";

});
```



弹出一个提示的对话框

```C++
//  已通过ui建立一个名字叫 actionopen 的对象
//  三个参数分别是： 父对象、窗口标题、提示文本
//  这些 QMessageBox::name -> return QMessageBox::StandardButton
//  按钮的触发是 &QAction::triggered

//  错误对话框
connect(ui.actionopen, &QAction::triggered, [this]() {
    QMessageBox::critical(this, "critical", "错误");
});

//  警告对话框
connect(ui.actionopen, &QAction::triggered, [this]() {
    QMessageBox::waring(this, "waring", "警告");
});

//  信息对话框
connect(ui.actionopen, &QAction::triggered, [this]() {
    QMessageBox::information(this, "info", "提示信息");
});

//  提问对话框  有两个按钮 ： yes  no
//  第四个参数 指定按键类型
//  第五个参数 默认关联回车的按键，默认是第一个键
connect(ui.actionopen, &QAction::triggered, [this]() {
    QMessageBox::question(this, "ques", "提问对话框",
    	QMessageBox::Save | QMessageBox::Cancel, QMessageBox::Save);
});
```



















