# <a name="sign">Verify Signature</a>

#### Rule

1. 参数名区分大小写；
2. key为自定义的私钥，可以为任何形式的字符，通信双方需要约定一致；

#### Step

1. 将参数名ASCII码从小到大排序（字典序）；
2. 使用‘&’和‘=’进行拼接
3. 拼接最后的自定义的key
4. 使用大写32位md5获得签名

#### Example：

一、需要传递的参数如下：

{  

​     "name":"foo",
​     "age":"2",
​     "username":"admin"
}



二、经过1.2两步之后得到的字符串为： age=2&name=foo&username=admin

三、经过第三步： age=2&name=foo&username=admin&key=XXX

四、经过第四部： sign = MD5(age=2&name=foo&username=admin&key=XXX)