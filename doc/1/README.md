# 第1天 

## 烂代码的例子

对接一个第三方平台 示例
```php
$config = [
    'appid' => 'xxx',
    'appkey' => 'xxx',
];
$api = new Api($config);
$api->put($localPath,$remotePath);
```

第一版需求 web端需要对接这个接口 你写了个web类xx方法实现功能,很简单就上线了

```php
class Web {

    public function xx(){
         $config = [
            'appid' => 'xxx',
            'appkey' => 'xxx',
        ];
        $api = new Api($config);
        $api->put($localPath,$remotePath);
        //...其他逻辑
    }
}
```

第二版需求 安卓端也需要对接这个接口,你又写了个Ad类xx方法实现功能,很简单就上线了

```php
class Ad {

    public function xx(){
         $config = [
            'appid' => 'xxx',
            'appkey' => 'xxx',
        ];
        $api = new Api($config);
        $api->put($localPath,$remotePath);
        //...其他逻辑
    }
}
```

第三版需求 需要将这个接口对外开放,你又写了个Api类xx方法实现功能,很简单就上线了

```php
class Api {

    public function xx(){
         $config = [
            'appid' => 'xxx',
            'appkey' => 'xxx',
        ];
        $api = new Api($config);
        $api->put($localPath,$remotePath);
        //...其他逻辑
    }
}
```



随着版本的迭代,你可能写了N个

突然有一天,appkey被谁给重置了

那就涉及到修改appkey了,可是一看,修改的地方实在是太多了

万一少改了一个呢? 批量修改? 

## 优化动机

当有一个参数需要修改时,改动的地方太多了,需要封装起来

## 优化后


先封装一个ApiUtils
```php
class ApiUtils {

    public static function getInstance(){
         $config = [
            'appid' => 'xxx',
            'appkey' => 'xxx',
        ];
        return new Api($config);
    }
}

```

调用


```php
class Web {

    public function xx(){
        $api = ApiUtile::getInstance();
        $api->put($localPath,$remotePath);
        //...其他逻辑
    }
}
```

这样不管有多少次调用,只需要修改 ApiUtils 中的配置就可以了


