1.在C/C++中，为了避免同一个文件被include多次，有两种方式：一种是#ifndef方式，一种是#pragma once方式(在头文件的最开始加入)。 #pragma once方式产生于#ifndef之后。#ifndef方式受C/C++语言标准的支持，不受编译器的任何限制；而#pragma once方式有些编译器不支持(较老编译器不支持，如GCC 3.4版本之前不支持#pragmaonce)，兼容性不够好。#ifndef可以针对一个文件中的部分代码，而#pragma once只能针对整个文件。

2.如果变量都是正数，那就用unsigned int，如果有正数或负数,那就用int

3.virtual bool meta_on_sign_save(){ return true; }//如果返回false会终止_sign_save
提供一个接口，且默认是返回true，继承后覆写可修改      

4.::可为全局作用域符号：当全局变量在局部函数中与其中某个变量重名，那么就可以用::来区分如：
例：
char    zhou;    //全局变量   如果全局变量在包含的文件中，也可以这么用
void    sleep（）
｛
      char    zhou;    //局部变量
     ::char(全局变量) =::char(全局变量) / char(局部变量);
｝

5.hpp，在boost、Xerces等开源库中频繁出现，hpp，其实质就是将.cpp的实现代码混入.h头文件当中，定义与实现都包含在同一文件，则该类的调用者只需要include该hpp文件即可，无需再将cpp加入到project中进行编译。而实现代码将直接编译到调用者的obj文件中，不再生成单独的obj，采用hpp将大幅度减少调用project中的cpp文件数与编译次数，也不用再发布烦人的lib与dll，因此非常适合用来编写公用的开源库。

6.#define后面的"\"是续行符，表示下面一行是紧接着当前行的，一般用于将十分长的代码语句分几段写（语句本身要求必须是一行,要注意\后面除了换行回车不能有任何字符，空格也不行：
  带参宏定义的一般形式为： 　#define 宏名(形参表) 字符串
　　宏名后的第一个括号就是参数，实际实用时，参数传入字符串中即可

8.startup是一个svr一个，声明要注册哪些消息处理函数,同时调用 gamer_rcf中的函数进行真正的注册(将处理函数和回复协议进行绑定得A，再用一个map存 请求协议=A)

9.typedef为C语言的关键字，作用是为一种数据类型定义一个新名字。这里的数据类型包括内部数据类型（int,char等）和自定义的数据类型（struct等）,用typedef只是对已经存在的类型增加一个类型名，而没有创造一个新的类型。只是增加了一个新名字，可以用该名字定义变量，   ;号结尾
例：
1.typedef int Status;  数据类型是int,新名字是status
2.typedef int NUM[100];//可看成 typedef int[100] NUM, int[100]是数据类型， num是新名字
  NUM n;
3.typedef struct  
{
    int month;
    int day;
    int year;  
} TIME;     TIME前的是数据类型，TIME是新名字
4.所以函数指针类型也是可以理解了

10.unordered_map和unordered_set的实现方式为哈希函数，不会根据key值对存储的元素进行排序。是计算元素的Hash值，根据Hash值判断元素是否相同。所以，
对unordered_map进行遍历，结果是无序的。  set没有key    stl::map是按照operator<比较判断元素是否相同，以及比较元素的大小，然后选择合适的位置插入到树中.所以，如果对map进行遍历（中序遍历）的话，输出的结果是有序的。
当不需要结果排好序时，最好用unordered_map。

11.#pragma  pack (push,1)     作用：是指把原来对齐方式设置压栈，并设新的对齐方式设置为一个字节对齐
相当于：
#pragma pack(push) //保存对齐状态
#pragma pack(4)//设定为4字节对齐
在代码结尾还有一个#pragma pack(pop) 表示恢复压入栈中的对齐状态

12.	net_base.h
	struct Msg;  //这属于前向声明，因为目地是声明一个指针，而指针都是4个字节，在声明指针时不需要提前知道这个指针指向的类型的大小。
	BOOSTSHAREPTR(Msg, ptrMsg);

13.DLL是Dynamic Link Library的缩写，意为动态链接库。在Windows中，许多应用程序并不是一个完整的可执行文件，它们被分割成一些相对独立的动态链接库，即DLL文件，放置于系统中。当我们执行某一个程序时，相应的DLL文件就会被调用。一个应用程序可有多个DLL文件，一个DLL文件也可能被几个应用程序所共用，这样的DLL文件被称为共享DLL文件。DLL文件一般被存放在C:WindowsSystem目录下。

14.为了在多线程使用全局变量或者静态变量时,线程间互不影响。  TLS线程本地存储。TLS的作用是能将数据和执行的特定的线程联系起来。 

15.IDL(Interface Definition Language)即接口定义语言，是CORBA规范的一部分，是跨平台开发的基础

16.RCF: 纯c++的RPC, 不引入IDL, 大量用到boost，比较强大.用于进程间通信

17.nedmalloc是一个跨平台的高性能多线程内存分配库

18.多线程内存池
　　直白的翻译：支持多线程安全操作的内存池。当然，我们不能够通过加锁的方式来获得安全；否则，我们只会做的更糟（会比系统的慢....可能）。

19.TLS（线程本地存储），如果代码支持多线程；那么，内存释放的时候，其绝对不会在原来分配时的线程.所以，我们需要一个合理且有效的模型：线程间内存池交换内存的模型——使用一个全局的共享内存池，然后各个线程内部的内存池，向其发起分配和释放的请求。这样，我们也就不在担心上面的问题了；我们可以通过这个全局池，来完成跨线程间的内存操作。当然，全局池需要加锁，这点毋庸置疑。为了减少加锁的消耗，我们可以缩短线程内部池的访问频率，比如：内部池的分配/释放频率与全局池的访问频率，比
例在：10000:1，或更高。这样，通过均摊，最后加锁的消耗，几乎完全没有了（即使消耗1ms，现在均摊后也只有0.1us）。
需要内存池的目地是提高性能，        影响内存池性能：控制住线程内部池向全局池的访问频率。

20.size_t:它是一种“整型”类型，里面保存的是一个整数，就像int, long那样。这种整数用来记录一个大小(size)。size_t的全称应该是size type，就是说“一种来记录大小的数据类型”。通常用sizeof(XXX)操作的结果就是size_t类型。因为size_t类型的数据是保存了一个整数，
所以它也可以做加减乘除，也可以转化为int并赋值给int类型的变量。

21.game_def文件夹中是定protocol，protocolID表示某条消息是什么类型的消息

22.一个最小的包是	:	unsigned short packageLen;  包的总长
					short protocolID;           消息类型 x2
					int	  netID;                什么用？？？？   process_id 命名空间中的，service_config
					int	  playerID;             玩家IGD
93.netid是表示是哪个服发的，是群发或http等;可看成是大范围的protocalID，

23.将可能出现异常的语句放在try{}中，当运行出现异常时，系统会抛出异常，再用catch{}来捕获抛出的异常。

24.bin文件夹是服务器的配置信息

25.类名（参数名）这样的对象是临时对象，不能取地址，不能被引用，不过可以给同类型的其他对象赋值，该临时对象定以后可以进行一次操作，然后立即销毁。当我们定义一个对象以后并不想立即给它赋初值，而是以后给它赋初值，在稍后赋初值的时候，该类临时对象就可以发挥作用了。
例：有一个类A;
A a;
a = A("one");

26.shared_ptr在定义的时候可以指定删除器（deleter）。无法直接传入析构函数。方法:在单例函数内部再定义一个Destory函数，该函数也要为static的，即通过类名可直接调用。

27.
weak_ptr被设计为与shared_ptr共同工作，可以从一个shared_ptr或者另一个weak_ptr对象构造，获得资源的观测权。但weak_ptr没有共享资源，它的构造/析构不
会引起指针引用计数的增加/减少。它只是一个静静地观察者。使用weak_ptr的成员函数use_count()可以观测
资源的引用计数，另一个成员函数expired()的功能等价于use_count() == 0，也就是shared_ptr管理的资源已经不复存在了。weak_ptr没有重载operator和->，它不共享指针，不能操作资源，这是它弱的原因。但它可以使用一个非常重要的成员函数lock()从被观测的shared_ptr获得一个可用的shared_ptr对象，从而操作资源。当expired() == true的时候，lock()函数将返回一个存储空指针的shared_ptr。

当两个对象需要互相引用的时候(各类中都有指针指向对方)，我们总希望其中一个对象拥有另外一个对象的强引用，而另外一个对象拥有自己的弱引用
可以使用lock获得一个可用的shared_ptr对象。weak_ptr的一个重要用途是通过lock获得this指针的shared_ptr,使对象自己能够生产shared_ptr来管理自己，

28.enable_shared_from_this是一个模板类
当类A被share_ptr管理，且在类A的成员函数里需要把当前类对象作为参数传给其他函数时，就需要传递一个指向自身的share_ptr。
1.为何不直接传递this指针
       使用智能指针的初衷就是为了方便资源管理，如果在某些地方使用智能指针，某些地方使用原始指针，很容易破坏智能指针的语义，从而产生各种错误。
2.可以直接传递share_ptr<this>么？
       不能，因为这样会造成2个非共享的share_ptr指向同一个对象，未增加引用计数导对象被析构两次。

29.playerDataPtr ptrOwnData = Own().getOwnDataPtr();
Own()中是取得playerDataPtr的指针，getOwnDataPrt返回shared_from_this（）;

30.使用extern和包含头文件来引用函数区别
extern的引用方式比包含头文件要简洁得多！想引用哪个函数就用extern声明哪个函数。一个明显的好处是，会加速程序的编译（确切的说是预处理）的过程间。在大型C程序编译过程中，这种差异是非常明显的。

31.lexical_cast 位于boost命名空间，为了使用 lexical_cast，需要包含头文件 <boost/lexical_cast.hpp>
1.lexical_cast在转换字符串时，字符串中只能包含数字和小数点，不能出现除e/E以外的英文字符或者其他非数字字符。
可将字符串转成int,long等：例: int a = lexical_cast<int>("123");      string 到 int
2.可将数字将成string 例： string str = lexical_cast<string>(123)     int 到  string

32.本地存储线程（thread local storage）来代替静态数据（有时也被成为特殊线程存储，thread-specific storage）
Boost线程库提供了智能指针boost::thread_specific_ptr来访问本地存储线程(哪个线程调用thread_specific_ptr,指针就指向谁的独立空间)。每一个线程第一次使用这个智能指针的实例时，它的初值是NULL，使用时先检查它的值是否为空，并且为它赋值。Boost线程库保证本地存储线程中保存的数据会在线程结束后被清除。

33....def  一般是enum和宏定义

35.申请空间后要用memset初始化，包括结构体

36.memcopy与memmove区别：当内存发生局部重叠的时候，memmove保证拷贝的结果是正确的，memcpy不保证拷贝的结果的正确

38.SINGLETON   提供一个static share()方法创建类的对象存在于栈中

39.	HeropartySide类中加了 属性加成这一特性，以后可能还要加其实特性，所以用struct ExAttriDetail {｝来描述每一个特性
    
41.bson目前主要用于mongoDB中，是mongoDB的数据存储格式。bson基于json格式，选择json进行改造的原因主要是json的通用性及json的schemaless的特性。

42.用malloc原因:失败返回null,提前知道内存有没有足够空间,将碎片空间进行整理成一个大块

44.asInt64：顾名思义，就是64位的int类型

45.pair是将2个数据组合成一个数据，当需要这样的需求时就可以使用pair，如stl中的map就是将key和value放在一起来保存。当一个函数需要返回2个数据的时候，可以选择pair。 pair的实现是一个结构体，主要的两个成员变量是first second 因为是使用struct不是class，所以可以直接使用pair的成员变量。

46.	const Json::Value &nw_js = cfgs["weight"];
	for (auto itr : nw_js) :json类型的数组居然也能用auto，顺序存储，有结尾的都能用？

48.namespace有 enum，namespace中可直接用enum中的值，namespace是class一样

49.其实在MongoDB里面，find()和findOne()的用法是一样的，举个例子：findOne({name:”mongo”})和find({name:”mongo”}).limit(1)其实是等效的。它们的参数也是一样的，只不过find()和findOne()返回的不同而已。
第一个区别就是，findOne()会返回符合条件的第一个文档对象，而find()会返回所有符合条件的对象数组。
第二个区别是，findOne()返回的是一个对象，而find()返回的是一个数组，数组里面装着对象。
findOne()返回的值前端只需要用data.name就能获取到，但find()返回的值前端要用data[i].name来获取。

60.MANTYPE  命名空间中，定义了英雄的enum,国籍，攻击类型，兵种,寻找目标优先级

61.取配置Common::loadJsonFile

63.creator是new一个类，并指明析构时调用的函数，返回指针，SINGLETON_PTR是new一个单例对象，返回对象

64.1.struct中全是publie，且没有构造函数，则可用｛｝进行构造，例：struct a = {}
	2.若struct中有private或protected，或有构造函数，则需使用构造函数进行初始化
例：
struct S {
    private:
        int x;
    public:
        double y;
        S(void){}
        S(int idemo,double ddemo) {x=idemo;y=ddemo;}
};
S os1;//将调用默认构造函数(无参构造函数)
S os2(1000,2.345);
S os3=S(2000,4.567);等价于：S os3(2000,4.567)  因是声明并初始化os3对象，所以将调用S(int,double)构造函数对os3进行初始化。
S os[4]={S(10,1.234),S(20,2.234)};//未初始化的将调用默认构造函数。如此时没有默认构造函数会出错。

但如果os3已经存在了，S os3(100,1.234);os3=S(2000,4.567)，则表示用一个临时对象赋值给os3，将调用operator=，然后系统再释放这个临时产生的对象。系统默认的=运算是将源对象的数据成员的值复制到目标对象中的数据成员中。
3.接受一个参数的构造函数允许使用赋值句法初始化对象。
例：class C {
    private:
        int x;
    public:
        C(int idemo) {x=idemo;}
};
C oc=1000;//不能加花括号

65. mongo::BSONObjBuilder,这是构建BSON对象的类     类：表示它提示了很多方法去添加数据，例apend(),或流<<

66.SINGLETONMUTEXPTRCREATE  看名，创建一把锁的指针，且是单例，所以返回是的share_ptr

67.	auto npc_json_list = Common::loadJsonFile("./instance/heroparty/robots.json");是加载本地的配置文件

68.	static json::value loadjsonfile(const std::string& file_name)   读取单个json文件 
static FileJsonSeq loadFileJsonFromDir(const std::string& files_path)   路径是一个目录，读取目录下的所有json文件

69.用map时，一般是是为了存类的ptr，类的空间用creator开辟,当有int能对应ptr时，可用unordermap，查找就通过int查找

72.	b.box1 = ActionBoxFormatFromJson(box_json1);传入宝箱的json数据，函数中会将box_json1的数据保存到变量boxdata中再返回

73.playerData是玩家的所有数据，包括玩法。

73.##是一个连接符号，用于把参数连在一起 ,#是“字符串化”的意思。出现在宏定义中的#是把跟在后面的参数转换成一个字符串
#define paster( n ) printf( "token " #n" = %d\n ", token##n ) 
所以paster(9);就是相当于 printf("token 9 = %d\n",token9);
 
74:stl：：set会排序

76.std::array中的data()，表示返回指向array中第一个元素的指针。
1. 读写锁机制
写者：写者使用写锁，如果当前没有读者，也没有其他写者，写者立即获得写锁；否则写者将等待，直到没有读者和写者。
读者：读者使用读锁，如果当前没有写者，读者立即获得读锁；否则读者等待，直到没有写者。

2. 读写锁特性：
同一时刻只有一个线程可以获得写锁，同一时刻可以有多个线程获得读锁。读写锁出于写锁状态时，所有试图对读写锁加锁的线程，不管是读者试图
加读锁，还是写者试图加写锁，都会被阻塞。
读写锁处于读锁状态时，有写者试图加写锁时，之后的其他线程的读锁请求会被阻塞，以避免写者长时间的不写锁。

76.typedef std::vector<mongo::BSONObj> objCollection;    

77.插入健值对  
mongo::BSONObjBuilder obj;   
    obj.append(strPlayerID, iPlayerID);
    插入值：
 mongo::BSONArrayBuilder attack_report;

78.整个整数 0x7FFFFFFF 的二进制表示就是除了首位是 0，其余都是1
就是说，这是最大的整型数 int（因为第一位是符号位，0 表示他是正数）

80.const static std::string strMsg = "msg";

81.静态成员变量不随对象的建立而分配空间的,也不是随对象的撤销而释放.静态成员变量是在程序编译时分配空间,而在程序结束时释放空间.

82.mongo::BSONObj key = BSON("key" << 1);
    mongo::BSONObj obj = BSON("key" << 1 << "ht" << HeroPartyCloseTime);
    在设置索引时，存的obj中，要存在该索引

83. player_mgr.getPlayer(iPlayerID);取玩家信息的接口，先在本地找，找不到再去DB取，不存在在不在线的问题，只有能取到数据或不能
 player_mgr.getOnlinePlayer();取在线玩家

84.gamer_data是玩家的基本信息，没有玩法，playerData是玩家的所有信息，包括玩法.但取时，都通过ptrPlayer指针，基本信息是ptrPlayer->Info().Face();

85. qValue json(qJson::qj_object);
    json.addMember(strMsg, list_json_send);在整合好要发送给gac的数据后，如果加了这两句，就可以调用sendToClient();

86.   action_mgr.RunBox(ptrPlayer, heroPartyBoxResPtr_ptr);调用这个接口，将bos(道具id,值)数组传入时，会自己添加到player的道具中

87.对heroparty的数据进行修改后，不但要将数据保存到dbs，还要发给gac进行更新

88.gac与gas的交换protocalID写在gate_game_protocal中

89.   PlayerDataInitial(playerBase, Info);  playerData中只是提供了初始化某些数据的接口，真正去调用的，是在玩家登录时，通过event_tick.cpp去处理

91.对于配置的信息，都是启服就下到本地中容器中。

92.auto_player在auto_base.h文件中，提供了下载db数据的虚函数的接口,因为玩家进入的时候，很多类都需要去数据中取数据，但实现的内容不同

94.gate将消息发给gg，gg的game_rcf进行处理，根据msg中的protocalid在func_keeper集合中找到注册的函数进行处理。
gg的所有gac的请求处理函数，都在startup中调用game_rcf的注册函数进行注册.定义protocolID是在gate_game_protocol中.在各具体的类中，是对处理函数进行实现，函数名就是注册时绑定的名。而处理玩家登录时，数据的加载和一些定时事件，是在event_tick中处理。

95.去找一个对象时，找不到返回share_ptr的null指针

96.消耗银两时，判断和消耗银两的接口，不知道还有什么资源是调用这个接口： const int cur_res = shops_mgr.checkCommon(cost, ownPlayer);

97.检查道具是否存在内存中和道具是否够的接口：    if (!Own().Items().overItem(star_config.cost_item, star_config.cost_num))

98. const Json::Value& sgJson = json["action"][n];
            if (sgJson.isMember("adjust"))
  sgJson是json类型时，isMember是判断它有没有这个字段

99."boxID2":[{"aid":17,"v":800},{"aid":1,"v":170000},{"aid":12,"vid":50048,"v":8},{"aid":2,"v":160}]
aid=17(群英币下没有选项，所以没有vid), aid=12(是道具，要有具体哪个道具，所以会有vid)

100.insert(pair<...>) 版本返回值是一个pair结构，其中第一个元素是一个迭代器，第二个元素是一个bool类型，如果原来的map中不含有插入的元素，则bool为true，迭代器指向插入的元素；如果map中已经含有插入的元素了，则bool为false，返回的迭代器指向对应的map中已经存在的元素

101:playerData *  和playerDataPtr是一样的：
  typedef boost::shared_ptr<playerData> playerDataPtr;

102. Json::Value& data_json = r[strMsg][1u] = Json::arrayValue;   注意这是1u的位置，发给gac，它想读就读
    Return(r, res); = r[strMsg][0u] = res;

103.1. 在使用merge功能时，一定要在合并目的地选择merge功能，而不是在数据源处选择merge。
2. 里面的from和to很容易被字面意思搞混，容易理解成“从。。到。。”。其实可以理解为，from为左边，起始状态，to为右边，最终状态。他们之间会做diff比较，之后将to的内容更新到from。
 
 172800  


问题：
1.头、源文件，编译，包含，继承
2.extern修饰函数时表示是在另一个文件中定义，thread_shared.h中，extern的函数在.cpp的文件中定义，还有必要加extren?

5.gamer.cpp   	16	static Gamer* SGT = NULL;   不是单例吗？为什么每次没析构就置空///static只会初始化一次,第二次并没有置空

7.ptrMsg ptr(new(nm)Msg(), delete_some<Msg>);  .h    52,  这样的类模版构造方式是什么意思？？？//new一个空间，但空间是外部传入的，
	构造成Msg()类型

12.time_mutex是在一定时间内没获取到互斥体就返回吗？-   是的，在一定时间内什么时候获得什么时候返回

15.	Json::Value data(Json::arrayValue);   int a = 0;   是初始化，传什么根据要存的值决定

17.heroparty_side   112   	ReadLock lock(mutex);    lock是局部变量，｛｝后会析构,锁即释放

18. 117  	today_js = Json::arrayValue;  不写不行吗？直接append不是会转成数组吗？ 初始化的意思，最好写

26.  102   heroparty_system.cpp  		
static SINGLETONMUTEXPTR SGM = SINGLETONMUTEXPTRCREATE(); 怎么用？是等待锁释放获得锁，才能执行线程吗？
		thread_shared::ExclusiveMutex(SGM);   所以线程共用这把锁，当其它线程在使用时，其它线程等待

29.heroparty_system取数据时的RandomAttriList权重是什么的权重，业务逻辑是什么？   

31.	SINGLETON(HeropartySide);生成的局部对象，是在关服才释放？  静态的，关服才释放

32.heroparty_system  145  					MAPWAR::armyNPC npc(npcJson);   为什么没有开辟堆空间？	mapDataPtr->npcList.push_back(npc);拷贝构造了一份，之前的可释放掉

34.	std::vector<mongo::BSONElement> ele = obj["old_rank"].Array();  array()什么作用？？ array()是转成c数组，arr()是转成json数组吗？

39.	if (!kFind["fightcd"].eoo()) { heroPartyPtr_ptr->uiFightCD = kFind["fightcd"].Int(); } --eoo（）判断字段是否存在
heroparty_system.cpp 451 

40.  heroparty_system.cpp 153   			int id = -1;   为怎么从-1开始减，影响效率吗？   robot  npc的id是-1开始

41.	thread_shared::GetLocalMongo().EnsureIndex(DBN::dbSeason, BSON("key" << 1));  DBN：：dbseason是一个集合

43.auto_do.cpp 25  
1.thread_shared::GetLocalHelper().meta_tick_save(getOwn());   线程用完就关，动态的开启和关闭


44.   objCollection obj = thread_shared::GetLocalMongo().Query(DBN::dbPlayerHeroParty);  请求的是一个集合还是一个数据库？？集合

45. heroparty_system.cpp 467   std::vector<mongo::BSONElement> elems = kFind["attack"].eoo() ? std::vector<mongo::BSONElement>() : kFind["attack"].Array();
为什么用bsonelement,用array或object不行吗？BSONElenment代表了array和object

49.什么时候用qvalue    效率高

50.  162 playerdata.h PlayerDataInitial(playerBase, Info);  怎么读？？定了些函数，在.cpp中才调用//注意.h中的宏定义，实现在.cpp文件中，
不能认为宏定义替换后的语句是上往下执行,调用才执行

52.307  playerManager.cpp     return playerDataPtr();   playerDataPtr不是模版类吗？为什么直接加（）是生成一个临时的指针吗？空指针，看share_ptr实现

56.  290    playerdata.cpp    void playerData::sendToClient(const short protocol, qValue& msg)
  void playerData::sendToClientFillMsg(const short protocol, qValue& msg) 这两个接口有什么区别？   一个加了Msg开头，一个没有加

57.  405   heroparty_system.cpp     ReadJsonArray;   这个怎么用？？相当于解包

58. 1094  heroparty_system.cpp    json[strMsg][0u] = err_heroparty_fight_chart_num; [1u]   json:value中有重载

62. void heroparty_system::get_chart(net::Msg& m, Json::Value& r).处理gac请求的函数必须这么写吗？声明的宏定义就是两个参数的，所以实现函数也是两个参数

63. 462   player_man.cpp      battle_value = STDMAX(0, battlevalue);    不是明白的0小吗？判断是否越界，一个有符号的正数越界后是负数

64. void man_system::manFriendUpgrade(net::Msg& m, Json::Value& r)   755    消耗银两后，怎么没有保存到db??


66.player_man.cpp  1379       man->meta_sign_auto();   自动保存玩家数据到db，自动同步到gac？涉及到玩家自己的数据就用这个，系统的数据需自实现吗？

67.       data_ptr->offsetCD = data_ptr->offsetCD > DAY ? DAY : data_ptr->offsetCD;   122 mall_system.cpp   

68.玩家中途进入是在哪执行5点的定时事件？？    -------玩家下线并不会执行定时事件，上线也不会主动去检测吗？

70.   extern void Log(const std::string table, playerDataPtr player, const int tag, std::string f1 = "", std::string f2 = "", std::string f3 = "", std::string f4 = "", std::string f5 = "", std::string f6 = "", std::string f7 = "", std::string f8 = "");
470   dbdriver    为什么存player，tag是什么作用            -----



[root@localhost:10.17.172.222 server]# gdb ./gg 31672

(gdb) l event_tick.cpp:576

(gdb) b event_tick.cpp:576

(gdb) c




gdb   core   json...    svn    screen  sendClient

aria2c -x 5 -c http://llvm.org/releases/3.9.0/cfe-3.9.0.src.tar.xz
