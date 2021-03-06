---
layout: page
title: 分享接口
nav-index: 10
---
分享的相关接口

获取我的分享
----------------
用户在表情meapp里分享

地址: `/v1/{app_id}/share/myshare`

方法: `GET`

说明: 用户登录后，获取他的最近100个分享

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken         |String  |用户登录令牌识别码    |*是   |


返回值:
{% highlight js %}
[
    {
        "sharetoken":"分享的token",
        "share_base_id":"分享根据id",
        "type":"分享的类型",
        "is_share_pwd":"此分享是否需要密码才能使用",
        "share_user_id":"此分享只能指定的用户使用",
        "share_count":"此分享最多使用多少次",
        "used_count":"此分享已经被多少人使用过了",
        "share_expire":"此分享过期时间",
        "write_time":"分享的创建时间",
        "img_url":"分享出去的图片url地址"
    }
    //...
]
{% endhighlight %}

发布一个新的分享
----------------

地址:`/v1/{app_id}/share/myshare`

方法:`POST`

说明: 在表情meapp里，分享出去一个新的

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken         |String  |用户登录令牌识别码    |*是   |
| type         |int  |分享的类型，1为角色，2为大头贴，3为表情    |*是   |
| share_base_id         |int  |根据分享类型不通，此字段为角色id，大头贴id，表情id    |*是   |
| share_pwd         |String  |此分享是否需要密码才能使用，这里传入使用密码    |否   |
| share_user_id        |String  |此分享只能指定的用户使用，这里传入这个人的用户id    |否   |
| share_count          |int  |此分享最多使用多少次，这里传入最多使用次数    |否   |
| share_expire         |int  |此分享过期时间，这里传入到期时间,到期时间以秒为单位的时间戳形式    |否   |


返回值:
{% highlight js %}
{
    "sharetoken":"新增分享的token的md5值",
    "share_url":"分享出去的落地页url地址"
}
{% endhighlight %}

删除我发布的一个分享
----------------

地址:`/v1/{app_id}/share/myshare"`

方法:`DELETE`

说明:需要签名

参数:

| url参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken         |String  |用户登录令牌识别码    |*是   |
| sharetoken         |String  |删除我的分享token    |*是   |


返回值:

    {}


使用发布的一个分享
----------------

地址:`/v1/share/useshare/{shareToken}`

方法:`POST`

说明: 不需要签名，需要登录

参数:

| url参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken         |String  |用户登录令牌识别码    |*是   |
| share_pwd         |String  |此分享是否需要密码才能使用，这里传入使用密码    |否   |
| from1         |String  |用户通过什么渠道获得的此分享，这里可以传入 weixin,qq等    |否   |
| from2         |String  |用户通过什么渠道获得的此分享，这里可以传入 weixin,qq等    |否   |


返回值:

    {}



获取的一个分享详细信息
----------------

地址:`/v1/share/get/{shareToken}`

方法:`GET`

说明: 不需要签名，不需要登录，给page页面使用展现

参数:

| url参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|


返回值:
{% highlight js %}
    {
        "sharetoken":"分享的token",
        "share_base_id":"分享根据id",
        "type":"分享的类型",
        "is_share_pwd":"此分享是否需要密码才能使用",
        "share_user_id":"此分享只能指定的用户使用",
        "share_count":"此分享最多使用多少次",
        "used_count":"此分享已经被多少人使用过了",
        "share_expire":"此分享过期时间",
        "write_time":"分享的创建时间",
        "img_url":"分享出去的图片url地址"
    }
    //...
{% endhighlight %}

