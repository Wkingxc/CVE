SQL injection vulnerability exists in ibos oa v4.5.5

official website:http://www.ibos.com.cn/

version:4.5.5

Function point: Integrated Office = "Notification Announcement =" Mobile notification

![WPS图片(1)](https://github.com/funnn7/cve/assets/139324696/853d0d2e-f986-4e2c-9698-64062f186040)

![WPS图片(2)](https://github.com/funnn7/cve/assets/139324696/dbe3ecc7-8595-47e1-a6c4-6c5ca55ccbe0)

POC

Routing: r = officialdoc officialdoc/edit

Successfully burst the database name by reporting an error injection

![WPS图片(3)](https://github.com/funnn7/cve/assets/139324696/2b8d70d4-1170-414f-8185-bdb3ebccb4bb)

Analyze

It's routed here and it calls the actionEdit() method, it selects the function point by passing in the op parameter and it calls move()
![WPS图片(4)](https://github.com/funnn7/cve/assets/139324696/80f6d29b-2524-44c0-8353-8814b3476c95)

Two arguments docids and catid are passed in the move() method where docids is injected, bringing the values of both arguments into the updateAllCatidByDocids() method.

![WPS图片(5)](https://github.com/funnn7/cve/assets/139324696/be1d456f-2dae-4608-8f7a-7f00446da5ef)

The SQL statement is executed using the updateAll() wrapper function

![WPS图片(6)](https://github.com/funnn7/cve/assets/139324696/2d3b2765-af31-4c8d-a954-d077c8fcc1c1)
