# <a name='sign'>Verify Signature</a>

#### Rule

1. Parameter names are case sensitive.

#### Step

1. Sort the parameter name ASCII code from from A-Z order.
2. Stitch with ‘&’ and ‘=’ .
3. Stitching the last <a href='#secret '>Secret </a> .
4. Get the signature using uppercase 32-bit MD5 .

#### Example：

一、The parameters that need to be passed (JSON) are as follows:

*{  "name":"foo", "age":"2", "username":"admin"}*



二、After the 1 and 2 step, the string obtained is： *age=2&name=foo&username=admin*

三、After the 3 step:： *age=2&name=foo&username=admin&**secret**=XXX*

四、After the 4 step： *sign = MD5(age=2&name=foo&username=admin&**secret**=XXX)*

