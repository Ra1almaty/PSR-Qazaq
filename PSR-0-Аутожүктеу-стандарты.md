Аутожүктеу стандарты
====================
 
Алдыңызда, класстардың аутожүктегішімен үйлесімді болуы үшін орындалуға тиіс талаптар.

Міндетті түрде [-Талап|Талаптар-]
---------

* Абсолютті есімдер кеңістігі және класс есімдері келесі құрылымға 
  сәйкес болу керек `\<Vendor Name>\(<Namespace>\)*<Class Name>`
* Әр есімдер кеңістігі жоғарғы деңгейлі есімдер кеңістігінен ("Vendor Name") тұру керек. 
* Әр есімдер кеңістігінде шектеусіз кіші буынды есімдер кеңістіктері бола алады. 
* Файл системасынан жүктелген кезде, есімдер кеңістігінің әр бөлгіші `DIRECTORY_SEPARATOR` бөлгішіне өзгертіледі.
* КЛАСС ЕСІМІНДЕГІ әр `_` симболы [-нышаны|рәмізі-] `DIRECTORY_SEPARATOR` бөлгішіне өзгертіледі. `_` симболы [-нышаны|рәмізі-] есімдер кеңістігінде арнайы бір мағынаға ие емес.
* Файл системасынан жүктелген кезде, Абсолютті есімдер кеңістігі мен класс `.php` суффиксімен толықтырылады
* Өндіруші [-вендор-], есімдер кеңістігі және класс атаулары кез келген қисындағы үлкен, кіші әріптердер тұра алады.

Мысалдар
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

Есімдер кеңістігі мен Класс Есімдеріндегі [-Класс Атауларындағы-] астыңғы сызба
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

Жоғарыда келтірілген стандарттар  аутожүктегішпен ауыртпалықсыз үйлесімдік орнату үшін қойылатын 
минималды ортақ келісімдер.
Осы стандарттарға сәйкестігіңізді, PHP 5.3 класстарын жүктей алатын - SplClassLoader орындалу нұсқасын қолданып тексере аласыз.

Орындалудың мысалы 
----------------------

Төмендегі нұсқалы функция - жоғарыдағы келтірілген стандарттардың қалай аутожүктелетінін көрсетеді

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
```

SplClassLoader Орындалуы
----------------------------- 
Келесі ұсынылған gist - жоғарыдағы станддартарға сүйенеген класстарды жүктей алатын SplClassLoader орындалым нұсқасы.
Бүгінгі таңдағы, осы стандарттарға сүйнетін PHP 5.3 класстарын жүктейтін ұсыным - осы. 

* [http://gist.github.com/221634](http://gist.github.com/221634)

