---
title: i山大APP源码解读
description: 阅读一下i山大源码
categories: 开发
tags:
  - Flutter
hide: true
abbrlink: 6052
---

## 概览

### 目录结构

```shell
├── api
│   ├── api.dart
│   ├── channel.dart
│   ├── event.dart
│   ├── request
│   │   ├── app_exceptions.dart
│   │   ├── http_request.dart
│   │   ├── http_utils.dart
│   │   └── interceptor
│   │       ├── cache_interceptor.dart
│   │       ├── error_interceptor.dart
│   │       ├── link_change_interceptor.dart
│   │       ├── request_interceptor.dart
│   │       └── retry_interceptor.dart
│   ├── server.dart
│   ├── todo_api.dart
│   └── wss.dart
├── bean
│   ├── bean.dart
│   ├── message_enum.dart
│   ├── result_entity.dart
│   ├── themes.dart
│   └── todo
│       ├── calendar_event.dart
│       ├── calendar_event.g.dart
│       ├── schedule_entity.dart
│       ├── schedule_entity.g.dart
│       ├── todo_item.dart
│       └── todo_item.g.dart
├── dialog
│   ├── label_choose_dialog.dart
│   ├── loading_dialog.dart
│   ├── notifacation_dialog.dart
│   ├── text_field_dialog.dart
│   └── todo_event_dialog.dart
├── main.dart
├── route
│   └── route_table.dart
├── settings
│   └── color_scheme.dart
├── ui
│   ├── about.dart
│   ├── academic.dart
│   ├── accountbill.dart
│   ├── activity.dart
│   ├── activityview.dart
│   ├── announce.dart
│   ├── attachment.dart
│   ├── audit_course.dart
│   ├── calendar.dart
│   ├── chat.dart
│   ├── courseselect.dart
│   ├── education_plan.dart
│   ├── evaluate.dart
│   ├── exam.dart
│   ├── feedback.dart
│   ├── grade.dart
│   ├── history.dart
│   ├── image.dart
│   ├── library.dart
│   ├── login.dart
│   ├── main.dart
│   ├── main_news.dart
│   ├── main_user.dart
│   ├── map.dart
│   ├── minor_login.dart
│   ├── minor_manage.dart
│   ├── more.dart
│   ├── news.dart
│   ├── origin.dart
│   ├── phone.dart
│   ├── privacy.dart
│   ├── schoolbus.dart
│   ├── search.dart
│   ├── settings.dart
│   ├── studyroom.dart
│   ├── timetable.dart
│   ├── todolist.dart
│   ├── tools
│   │   ├── code_conversion.dart
│   │   ├── force_exit.dart
│   │   ├── random_choose.dart
│   │   ├── reflection_test.dart
│   │   └── tools.dart
│   ├── user.dart
│   ├── volunteer.dart
│   └── yb.dart
├── util
│   ├── cache_util.dart
│   ├── clipboard_util.dart
│   ├── comm.dart
│   ├── converter.dart
│   ├── course_api_channel.dart
│   ├── database_util.dart
│   ├── device_info.dart
│   ├── device_info_util.dart
│   ├── font_util.dart
│   ├── global_message.dart
│   ├── icon_util.dart
│   ├── image.dart
│   ├── intercept_single.dart
│   ├── log_util.dart
│   ├── notification.dart
│   ├── notification_util.dart
│   ├── package_info_util.dart
│   ├── path_util.dart
│   ├── permission_util.dart
│   ├── platform_util.dart
│   ├── security_util.dart
│   ├── sentry_util.dart
│   ├── sharedpreference_util.dart
│   ├── shortcuts_util.dart
│   ├── store.dart
│   ├── string_util.dart
│   └── ws.dart
└── widget
    ├── app_bar.dart
    ├── cards.dart
    ├── constants.dart
    ├── delegate_builder.dart
    ├── function_widget.dart
    ├── head_image.dart
    ├── html_widget.dart
    ├── list_title_switch.dart
    ├── marquee_text.dart
    ├── rich_text.dart
    ├── sducalendar.dart
    ├── shape.dart
    ├── toast.dart
    └── view_image.dart

```

i山大目录有以下几个主目录

- api: 网络api。
- bean: 实体类。
- dialog: 封装后的提醒事项。
- route: 存放路由表。
- settings: 已废弃，用于配置配色。
- ui: 构建UI。
- util: 缓存管理、粘贴板管理等工具。
- widget: 存放自行封装的卡片、富文本等Widget。

### 依赖情况

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter

  dio: ^4.0.0
  sqflite: ^2.0.2
  path_provider: ^2.0.9
  shared_preferences: ^2.0.5
  url_launcher: ^6.0.10
  flutter_slidable: ^1.3.0
  image_picker: ^0.7.4
  file_picker: ^4.5.1
  flutter_downloader: ^1.6.0-nullsafety.0
  event_bus: ^1.1.0
  photo_view: ^0.4.2
  marquee: ^1.6.1
  date_format: ^1.0.8
  flutter_sticky_header: ^0.6.1
  web_socket_channel: ^1.0.13
  flutter_speed_dial: ^6.0.0
  pull_to_refresh: ^2.0.0
  # for update
  flutter_local_notifications: ^5.0.0+4
  permission_handler: ^7.1.0
  share_plus: ^4.0.9
  device_info_plus: ^3.2.2
  # 只有这个版本可以
  package_info_plus: '1.3.0'
  hive: ^2.1.0
  hive_flutter: ^1.1.0
  smooth_page_indicator: ^0.2.0
  material_floating_search_bar: ^0.2.6
  flutter_inappwebview: ^5.3.2
  amap_flutter_map: ^2.0.1
  reorderables: ^0.5.0
  get: ^4.6.5
  expansion_tile_card: ^2.0.0
  quick_actions: ^0.6.0+2
  connectivity_plus: ^1.1.0
  # 格式化日期时间等
  intl: ^0.17.0
  path: ^1.8.0
  fl_chart: ^0.55.0
  sentry_flutter: ^6.6.0
  json_serializable: ^3.5.1
  json_annotation: ^3.1.1
  r_calendar: ^0.1.11
  # for news
  flutter_widget_from_html_core: ^0.8.5+3
  fwfh_selectable_text: ^0.8.3
  sanitize_html: ^2.0.0
  image: ^3.1.3
  flutter_breadcrumb: ^1.0.1
  bottom_sheet: ^3.1.1
  flutter_staggered_animations: ^1.0.0
  flutter_staggered_grid_view: ^0.6.1

  # for desktop
  bot_toast: ^4.0.2
  extended_image: ^6.2.1

  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.0

dev_dependencies:
  build_runner: ^1.10.4
  msix: ^3.1.4
  flutter_test:
    sdk: flutter
```

### APP启动流程

观摩一下`main.dart`

```dart
//捕获Flutter框架异常
Future<Null> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await initialize();
  FlutterError.onError = (FlutterErrorDetails details) async {
    if (isInDebugMode) {
      FlutterError.dumpErrorToConsole(details);
    } else {
      Zone.current.handleUncaughtError(details.exception, details.stack);
    }
  };

  // ...

}
```

首先注意到`WidgetsFlutterBinding.ensureInitialized();`这条语句，在讨论他之前，需要看一下一个Flutter项目是如何跑起来的。

众所周知，Flutter的入口也是`main()`函数，并在内部调用`runApp()`方法装载Widget。这个机制给出了一种问题的解决：

当App启动需要进行数据加载或网络请求时，可以使用多次运行`runApp()`的方式建立一个空白的等待页[^1]

```dart
void main() {
  runApp(const SplashScreen());

  Future.delayed(Duration(seconds: 10), () {
       runApp(const MyApp());
   });
}
```

至于`runApp()`函数，可以查看他的源码

```dart
void runApp(Widget app) {
  WidgetsFlutterBinding.ensureInitialized()
  ..scheduleAttachRootWidget(app)
  ..scheduleWarmUpFrame();
}
````

一共有三个阶段组成

1. `WidgetsFlutterBinding`初始化（`ensureInitialized()`）,与 `Flutter Engine` 进行通信。
2. 绑定根节点创建flutter著名的三棵树（`scheduleAttachRootWidget(app)`）进行布局。
3. 将布局出来的树进行渲染（`scheduleWarmUpFrame()`）

另外参考StackOverflow上的一个回答：

The above image is the architecture layers of Flutter, the `WidgetFlutterBinding` is used to **interact with the Flutter engine**. `Firebase.initializeApp()` needs to call native code to initialize Firebase, and since the plugin needs to use platform channels to call the native code, which is done asynchronously therefore you have to call `ensureInitialized()` to **make sure that you have an instance** of the `WidgetsBinding`[^2].

之后会异步调用`initialize()`方法。

接下来调用`FlutterError.onError()`方法捕获异常。所有 Flutter 的错误均会被回调方法 `FlutterError.onError` 捕获。默认情况下，会调用 `FlutterError.presentError` 方法，并将错误转储到当前的设备日志中。当从 IDE 运行应用时，检查器重写了该方法，错误也被发送到 IDE 的控制台，可以在控制台中检查出错的对象[^3]。

例如，如果你想在 release 模式下发生错误时立刻关闭应用，可以使用下面的回调方法:

```dart
void main() {
  FlutterError.onError = (FlutterErrorDetails details) {
    FlutterError.presentError(details);
    if (kReleaseMode)
      exit(1);
  };
  runApp(MyApp());
}
```

i山大将判断是否为`debug`模式，若是则直接输出到console，否则的话调用`Zone.current.handleUncaughtError(details.exception, details.stack)`

接下来在`Zone`中捕获其他异常，并使用Sentry发送到报错平台

```dart
  runZonedGuarded(
    () {
      SentryFlutter.init((options) {
        options
          ..dsn =
              'http://61f9001280de456f8cadd3b013ad2fff@sentry.swsdu.online:9000/2';
        options.debug = isInDebugMode;
        options.useFlutterBreadcrumbTracking();
        options.beforeSend = beforeSend;
      }, appRunner: () => runApp(ISDUApp()));
    },
    (exception, stackTrace) {
       _reportError(exception, stackTrace);
    },
  );
```

下面添加发送报错前的信息

```dart
/// 发送错误前插入用户学号信息以及ip信息
FutureOr<SentryEvent> beforeSend(SentryEvent event, {dynamic hint}) async {
  event = event.copyWith(
      user: SentryUser(
          username: UserAPI.curUser?.casId ?? 'none', ipAddress: '{{auto}}'));
  return event;
}
```

顺便还有这两个函数

```dart
//反馈异常
void _reportError(Object exception, StackTrace stackTrace) async {
  LogUtil.log(exception, name: '_reportError');
  Sentry.captureException(exception, stackTrace: stackTrace);
}

bool get isInDebugMode {
  // 之前用的assert,感觉不够高级,还是这个好
  return kDebugMode;
}
```

下面是`main()`中调用的`initialize()`的细节

```dart
///初始化启动服务
Future<void> initialize() async {
  //并行初始化
  await Future.wait([
    Store.initialize(),
    SharedPreferenceUtil.initialize(),
    PackageInfoUtil.initialize(),
    DeviceInfoUtil.initialize()
  ]);
  // 下面务必在SharePreferenceUtil初始化完成后执行
  //加载原生channel
  NativeChannel.initialize();
  // 加载字体
  await FontUtil.initialize();
  HttpUtils.init(
      baseUrl: Server.baseHost, connectTimeout: 7500, receiveTimeout: 7500);
  if (PlatformUtil.isMobile) {
    await FlutterDownloader.initialize(debug: false);
  }
}
```

最后是整个App的Widget，首先`new`了个`botToastBuilder`用于生成提醒。然后是初始化设置函数

```dart
  ///初始化设置
  void initSetting() {
    // 初始化SharedPreference
    SharedPreferences s = SharedPreferenceUtil.instance;
    // 初始化控制缓存状态的参数
    if (s.getBool(SharedPreferenceUtil.CACHE_EXAM) == null) {
      s.setBool(SharedPreferenceUtil.CACHE_EXAM, true);
    }
    if (s.getBool(SharedPreferenceUtil.CACHE_SCHEDULE) == null) {
      s.setBool(SharedPreferenceUtil.CACHE_SCHEDULE, true);
    }
    // 初始化偏好功能的默认菜单
    if (s.getStringList(SharedPreferenceUtil.FAVOR_FUNCTION) == null) {
      s.setStringList(
          SharedPreferenceUtil.FAVOR_FUNCTION, ['图书馆', '自习室', '校车']);
    }
  }

  @override
  StatelessElement createElement() {
    //获取通知列表
    NotificationUtil.initNotification();
    // 加载用户信息
    UserAPI.fetchUserInformationString();
    //初始化WebSocket
    ChatWebSocket.initialize();
    initSetting();
    return super.createElement();
  }
```

最后，`build()`

```dart
@override
Widget build(BuildContext context) {
  return GetMaterialApp(
    title: 'i山大',
    //去除debug标志
    debugShowCheckedModeBanner: false,
    //支持自定义字体
    theme: FontUtil.merge(Themes.themeNow),
    //适配手机暗夜模式
    darkTheme: Themes.darkTheme,
    //添加国际化支持
    localizationsDelegates: [
      GlobalMaterialLocalizations.delegate,
      GlobalWidgetsLocalizations.delegate,
      GlobalCupertinoLocalizations.delegate,
    ],
    supportedLocales: [
      const Locale('zh', 'CN'),
      const Locale('en', 'US'),
    ],
    locale: Locale('zh'),
    onGenerateRoute: RouteTable.generateRoute,
      builder: (context, child) {
      double scale = SharedPreferenceUtil.instance
                .getDouble(SharedPreferenceUtil.TEXT_SCALE) ??
            1;
      return MediaQuery(
        key: UniqueKey(),
        data: MediaQuery.of(context).copyWith(textScaleFactor: scale),
        child: botToastBuilder(context, child),
      );
    },
    navigatorObservers: [
      SentryNavigatorObserver(),
      BotToastNavigatorObserver(),
    ],
    home: MainPage());
}
```

#### 关于WidgetsFlutterBinding

`WidgetsFlutterBinding`将是Widget架构和Flutter Engine连接的核心桥梁，也是整个Flutter应用层的核心。通过 `ensureInitialized()` 方法我们可以得到**一个全局单例**`WidgetsFlutterBinding`[^1]。

有时候我们会在发现有的app在在**运行应用程序之前先与Flutter Engine进行通信**，所以要先将`WidgetsFlutterBinding.ensureInitialized()`提前。

稍微解释一下各种Binding的作用。

- `ServicesBinding`：Flutter System 平台消息监听绑定类。即Platform与Flutter Layer通信相关服务，同时注册并监听应用生命周期回调。
- `SchedulerBinding`：Flutter 绘制调度器相关绑定类，调试统计绘制过程持续时间等编译模式下的操作。
- `GestureBinding`：Flutter Gesture事件绑定，处理屏幕事件分发和事件回调，其初始化方法的关键点是回调事件处理`_handlePointerDataPacket`函数被赋值给window的属性，以便window在接收到屏幕事件后调用，window的实例是 Framework Layer 和 Engine 桥接层用来处理屏幕事件。
- `RendererBinding`：引擎之间的渲染树和Flutter Binding类，内部重点是持有渲染树的根节点。
- `SemanticsBinding`：引擎之间的语义树和 Flutter Binding 类。

#### 使用`Zone`捕获并处理异常

Zone表示一个代码执行的环境范围，为了方便理解，读者可以将Zone类比为一个代码执行沙箱，不同沙箱的之间是隔离的，沙箱可以捕获、拦截或修改一些代码行为，如Zone中可以捕获日志输出、Timer创建、微任务调度的行为，同时Zone也可以捕获所有未处理的异常[^4]。Dart中有一个`runZoned()`方法，可以给执行对象指定一个Zone。

在Flutter中，还有一些Flutter没有为我们捕获的异常，如调用空对象方法异常、Future中的异常。在Dart中，异常分两类：同步异常和异步异常，同步异常可以通过try/catch捕获，而异步异常则比较麻烦，如下面的代码是捕获不了Future的异常的:

```dart
try{
    Future.delayed(Duration(seconds: 1)).then((e) => Future.error("xxx"));
}catch (e){
    print(e)
}
```

如果你想捕获这样的错误，请使用 `runZonedGuarded()`。

```dart
void main() {
  runZonedGuarded(() {
    runApp(MyApp());
  }, (Object error, StackTrace stack) {
    myBackend.sendError(error, stack);
  });
}
```

> 请注意，如果你的应用在 `runApp` 中调用了 `WidgetsFlutterBinding.ensureInitialized()` 方法来进行一些初始化操作（例如 `Firebase.initializeApp()`），则必须在 runZonedGuarded 中调用 `WidgetsFlutterBinding.ensureInitialized()`

## 路由

`RouteTable`类维护一个`Map`作为路由表

```dart
//路由界面a-z排序
  static Map<String, WidgetBuilder> _routes = {
    //主界面
    '/': (context) => MainPage(),
    //教务
    'academic_page': (context) => AcademicPage(),
    // ...
    //志愿查询
    'volunteer_page':(context) => VolunteerPage(),
  };
```

以及一个鉴权拦截表，用于判断页面是否需要登录

```dart
  //鉴权拦截表
  static Map<String, bool> _needLogin = {
    //主界面
    '/': false,
    //教务
    'academic_page': true,
    // ...
    //志愿查询
    'volunteer_page': true,
  };
```

这里需要插入介绍`MaterialApp`接受的`onGenerateRoute`参数。它可以传参，相比于命名路由，可以多做一些相关的拦截[^6]，比如[^7]

```dart
MaterialApp(
  // Provide a function to handle named routes.
  // Use this function to identify the named
  // route being pushed, and create the correct
  // Screen.
  onGenerateRoute: (settings) {
    // If you push the PassArguments route
    if (settings.name == PassArgumentsScreen.routeName) {
      // Cast the arguments to the correct
      // type: ScreenArguments.
      final args = settings.arguments as ScreenArguments;

      // Then, extract the required data from
      // the arguments and pass the data to the
      // correct screen.
      return MaterialPageRoute(
        builder: (context) {
          return PassArgumentsScreen(
            title: args.title,
            message: args.message,
          );
        },
      );
    }
    // The code only supports
    // PassArgumentsScreen.routeName right now.
    // Other values need to be implemented if we
    // add them. The assertion here will help remind
    // us of that higher up in the call stack, since
    // this assertion would otherwise fire somewhere
    // in the framework.
    assert(false, 'Need to implement ${settings.name}');
    return null;
  },
)
```

因此路由表提供了一个方法生成一系列路由并进行鉴权

```dart
static Route generateRoute(RouteSettings settings) {
  // 路由名称未出现在路由表里,返回空界面
  if (!_routes.containsKey(settings.name)) {
    return MaterialPageRoute(
        builder: (_) => Scaffold(
          appBar: AppBar(title: Text('Not fount'),),
              body: Center(
                child: Text('No route defined for ${settings.name}'),
              ),
            ));
  }
  if (UserAPI.curUser == null && (_needLogin[settings.name] ?? false)) {
    return MaterialPageRoute(
        builder: (context) => LoginPage(), settings: settings);
  } else {
    return MaterialPageRoute(
        builder: _routes[settings.name], settings: settings);
  }
}
```

## 网络API

`api`包下结构是这个样子

```shell
├── api.dart
├── channel.dart
├── event.dart
├── request
│   ├── app_exceptions.dart
│   ├── http_request.dart
│   ├── http_utils.dart
│   └── interceptor
│       ├── cache_interceptor.dart
│       ├── error_interceptor.dart
│       ├── link_change_interceptor.dart
│       ├── request_interceptor.dart
│       └── retry_interceptor.dart
├── server.dart
├── todo_api.dart
└── wss.dart
```

### api及相关类

i山大在`server.dart`文件中管理服务器信息

```dart

class Server {
  static SharedPreferences _sharedPreferences;

  static final String hostSub = "https://sduonline.cn/isdudb_main";
  static final String hostMainStatic = "https://sduonline.cn/isduapp_static";

  static final String calendarConfigUrl = "https://widealpha.top/xl.config";

  static final String wsServer = 'wss://sduonline.cn/wss/';

  /* **********************************
   *下面的是2020新接口的host
   ********************************** */
  //主站域名,更新这个的时候一定要把../android/ui/ScheduleWidgetService里的变量一并更改
  static const List<String> baseHostList = [
    "https://inner.sduonline.cn", //内网线路
    "https://sduonline.cn", //外网线路一
    "https://isdu.swsdu.online", //外网线路二
  ];
  // 以下用于构建URL
  static String baseHost = "https://sduonline.cn";
  //  子服务的 URL
  static String hostAuth = "/isduapi/api/auth";
  static String hostCommonQuery = "/isduapi/api/common";
  static String hostEdu = "/isduapi/api/edu";
  static String hostUser = "/isduapi/infra/user";
  static String hostYiBan = "/isduapi/api/yiban";
  static String hostLibrary = "/isduapi/api/library";
  static String hostTool = '/isduapi/api/tool';

  static String _onlineServerAlive = '${Server.hostCommonQuery}/feedback/types';

  //检查是否是校园网
  static Future<bool> isSchoolNetwork() async {
    bool _isSchoolNetwork = true;
    //这个接口只是为了检查是否为内网情况，没有什么特殊意义
    //不使用封装的dio，避免被一直重发
    await Dio().get('http://urp.sdu.edu.cn/').catchError((obj) {
      _isSchoolNetwork = false;
    });
    return _isSchoolNetwork;
  }
}
```

问题来了，我也不知道前面几个接口是干嘛用的。留个坑。

判断校园网的逻辑很简单，发个请求，如果`Dio`catch到异常就说明不是校园网。

`api.dart`组织了所有API，首先看一下获取的Cookie的API。i山大一共需要获取三个Cookie，分别是`serviceCookie`、`educationCookie`和`dataCenterCookie`，分别对应学校提供的三个主要服务。以获取`serviceCookie`为例

```dart

///Cookie接口
class CookieAPI {
  // 组装三个服务的登录URL
  static String _service = '${Server.hostAuth}/login/service';
  static String _edu = '${Server.hostAuth}/login/edu';
  static String _data = '${Server.hostAuth}/login/data_center';

  // 异步获取Cookie
  static Future<Map<String, String>> serviceCookie() async {
    Box _hiveBox = await Hive.openBox('pBox',
        encryptionCipher: HiveAesCipher(
            SecurityUtil.generateKeyByString(UserAPI.curUser.casId)));
    Response response = await HttpUtils.post(_service, params: {
      'u': _hiveBox.get('u'),
      'p': _hiveBox.get('p'),
    });
    return _generateCookieMap(response.data ?? '');
  }

  static Future<Map<String, String>> educationCookie() async {
    // ...
  }

  static Future<Map<String, String>> dataCenterCookie() async {
    // ...
  }

  static Map<String, String> _generateCookieMap(String cookie) {
    Map<String, String> map = {};
    cookie.split(';').forEach((element) {
      try {
        if (element.isNotEmpty) {
          Cookie c = Cookie.fromSetCookieValue(element ?? '');
          map[c.name] = c.value ?? '';
        }
      } catch (e) {
        map[element] = '';
      }
    });
    return map;
  }
}
```

其中

```dart
Box _hiveBox = await Hive.openBox(
  'pBox',
  encryptionCipher: HiveAesCipher(
    SecurityUtil.generateKeyByString(
      UserAPI.curUser.casId)));
```

使用`Hive`的`encrptedBox`，通过封装的`SecurityUtil`工具计算AES获得i山大登录信息，并将其装载到URL中通过HttpUtil请求Cookie。

i山大使用这几个方法获取登录Token。其中`minorToken`是辅修使用的Token。

```dart
  static Future<String> getToken() async {
    bool isMinor = await Store.getBool('isMinor') ?? false;
    return isMinor ? await getMinorToken() : await getMainToken();
  }

  static Future<String> getMinorToken() async {
    String token;
    token = await Store.get('minorToken');
    return token;
  }

  static Future<String> getMainToken() async {
    String token;
    token = await Store.get('token');
    return token;
  }
```

使用refreshToken更新Token的方法

```dart
  ///获取refresh_token,并存储到数据库中
  static Future<bool> refreshTokens() async {
    bool isMinor = await Store.getBool('isMinor') ?? false;
    String refreshToken = isMinor
        ? await Store.getString('minorRefreshToken')
        : await Store.getString("refresh_token");
    if (refreshToken == null || refreshToken.isEmpty) {
      return true;
    }
    Response response = await HttpUtils.post(_refresh,
        data: FormData.fromMap({
          'refresh_token': refreshToken,
          'k': await DeviceInfoUtil.getUniqueId()
        })).catchError((error) {
      LogUtil.log(error, name: 'UserAPI.getRefreshToken');
      return Response(requestOptions: error.requestOptions, data: {
        'code': -1,
      });
    });
    if (response.data['code'] == -1) {
      LogUtil.log('refreshToken请求异常', name: 'UserAPI.getRefreshToken');
      return false;
    }
    if (response.data['code'] == 40102) {
      Fluttertoast.showToast(msg: '登录已失效,请退出并重新登录账户');
      return false;
    }
    var result = JsonDecoder().convert(response.toString());
    if (result != null) {
      if (result['code'] != 0) {
        return true;
      }
      if (isMinor) {
        await Store.set('minorToken', result['data'][0]);
        await Store.set('minorRefreshToken', result['data'][1]);
      } else {
        await Store.set('token', result['data'][0]);
        await Store.set('refresh_token', result['data'][1]);
      }
    } else {
      return true;
    }
    return false;
  }
```

#### 使用Hive并加密[^8]

Sometimes it is necessary to store data securely on the disk. Hive supports **AES-256 encryption** out of the box (literally).

The only thing you need is a **256-bit (32 bytes) encryption key**. Hive provides a helper function to generate a secure encryption key using the Fortuna random number generator.

```dart
void main() async {
  const secureStorage = FlutterSecureStorage();
  // if key not exists return null
  final encryprionKey = await secureStorage.read(key: 'key');
  if (encryprionKey == null) {
    final key = Hive.generateSecureKey();
    await secureStorage.write(
      key: 'key',
      value: base64UrlEncode(key),
    );
  }
  final key = await secureStorage.read(key: 'key');
  final encryptionKey = base64Url.decode(key!);
  print('Encryption key: $encryptionKey');

  final encryptedBox= await Hive.openBox(
    'vaultBox', 
    encryptionCipher: HiveAesCipher(encryptionKey));
  encryptedBox.put('secret', 'Hive is cool');
  print(encryptedBox.get('secret'));
}
```

### 拦截器

## 参考资料

[^1]: [Flutter runApp -- WidgetsFlutterBinding - 掘金](https://juejin.cn/post/7031196891358429220)

[^2]: [What Does WidgetsFlutterBinding.ensureInitialized() do? - StackOverflow](https://stackoverflow.com/q/63873338/19503179)

[^3]: [在Flutter里处理错误](https://flutter.cn/docs/testing/errors)

[^4]: [Flutter异常捕获](https://book.flutterchina.club/chapter2/thread_model_and_error_report.html)

[^5]: [runZonedGuarded<R> function - Flutter](https://api.flutter-io.cn/flutter/dart-async/runZonedGuarded.html)

[^6]: [Flutter onGenerateRoute 路由管理 - CSDN](https://blog.csdn.net/sinat_17775997/article/details/106687888)

[^7]: [给特定的 route 传参 - Flutter](https://flutter.cn/docs/cookbook/navigation/navigate-with-arguments)

[^8]: [Encrypted box - Hive](https://docs.hivedb.dev/#/advanced/encrypted_box)
