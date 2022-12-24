# Get about date

```
        let d = new Date();
        let year = d.getFullYear();
        // let month = d.getMonth();
        let day = d.getDay();
        let month = d.getUTCMonth() + 1;
        let UTCDate = d.getDate();
```

# How could we call APEX in LWC

in APEX Class

```
        /**
        * @description
        */
        public with sharing class UseWire {
        /**
        * @description getContacts description
        * @return   return List<Contact> contacts
        */
        @AuraEnabled(cacheable=true)
        public static List<Contact> getContacts() {
                try {
                List<Contact> contacts = [
                        SELECT AccountId, Email, Phone
                        FROM Contact
                ];
                return contacts;
                } catch (Exception e) {
                throw new AuraHandledException(e.getMessage());
                }
        }
        // public useWire() {

        // }
        }

```

In LWC JS

```

        import { LightningElement, wire } from "lwc";
        import getContacts from "@salesforce/apex/UseWire.getContacts";
        import refreshApex from "@salesforce/apex";
        export default class sfdxDisplayContacts extends LightningElement {
                contacts;
                error;

                @wire(getContacts)
                wiredContacts({ error, data }) {
                        console.log("this.wiredContacts: ", { error, data });
                        if (data) {
                        this.contacts = data;
                        this.error = undefined;
                        } else if (error) {
                        this.error = error;
                        this.contacts = undefined;
                        }
                }
                refreshContact() {
                        refreshApex(this.wiredContacts);
                }
        }

```

# How Could RefreshApex in the before.

# How to solve use github with VS Code problems about :

## unable to access 'https://github.com/creator-t/The-World-Of-tk.git/': SSL certificate problem: self signed certificate in certificate chain

Open Git Bash and run the command if you want to completely disable SSL verification.

```

        git config --global http.sslVerify false

```

Note: This solution opens you to attacks like man-in-the-middle attacks. Therefore turn on verification again as soon as possible:

```

        git config --global http.sslVerify true

```

I edited the Git config text file
C:\Users\ktian019\.gitconfig(PWC's computer)

## fatal: unable to update url base from redirection:asked for: https://github.com/creator-t/The-World-Of-tk.git/info/refs?service=git-upload-pack redirect: http://20.205.243.166:6080/php/urlblock.php?args=AAAAdwAAABD1g1qsIMdXkmuj8XFsDa71AAAAEBuxrr~3vihwHGfXWfc~KucAAABHAAAAR7N0GUoICYSeh7z~iNQoJbFO4wLDqFZWEl5UAdKKCjgFnZ202k38TV67L1ABrcdQD1EK~oGi9ky~unYZEqRMPuiTPXXwqDEw&url=https://github.com%2fcreator-t%2fThe-World-Of-tk.git%2finfo%2frefs%3fservice%3dgit-upload-pack

```

        //I connect email and name
        git config --global user.email "you@example.com"
        git config --global user.name "Your Name"

```

the point is PWC blocks access to github, so log in to GitHub on your browser first, then sync.

# LWC Communication https://lwc.dev/guide/composition

## Parent to child

First Step:
Child: use @api to expose public variables and/or functions

```

        @api variables;

```

```

        @api
        function(){
                this.timestamp = new Date();
        }

```

Second Step:
Parent: pass variable in tag, and gain lwc dom to operate public function in js.
@api
unended

# Salesforce defined name about APEX Class and LWC

Use the project name as a prefix, followed by the class name or the name of the LWC, depending on the name.
such as:

```

        projectFirstClass

        projectFirstLWC

```

# LWC's LWCName.js-meta.xml

```

        <?xml version="1.0" encoding="UTF-8"?>
        <LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">
        <apiVersion>55.0</apiVersion>
        <isExposed>true</isExposed>
        <!--The title of the component. Appears in list views, like the list of Lightning Components in Setup, and in the Lightning App Builder and in Experience Builder.-->
        <masterLabel>Title</masterLabel>
        <targets>
                <target>lightning__AppPage</target>
                <target>lightning__RecordPage</target>
                <target>lightning__HomePage</target>
        </targets>
        </LightningComponentBundle>

```

# Delete a LWC From Project

First step:Deploy source to org
Second step:Delete from project and org(Delete else thing in org such as:page etc.)

# Documentation about salesforce

https://pmd.github.io/latest/pmd_rules_apex_documentation.html

# Use VPN

https://github.com/vpncn/vpncn.github.io

# Calendar

```

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Document</title>
            <style>
                    .wrap {
                    width: 600px;
                    border: 5px solid rgb(253, 108, 108);
                    border-radius: 20px;
                    margin: 50px auto;
                    padding: 20px;
                    background-color: rgb(10, 188, 242);
                }

                .head {
                    display: flex;
                    justify-content: space-between;
                    padding: 10px;
                    border-bottom: 3px solid rgb(253, 108, 108);
                }

                .title {
                    display: flex;
                    justify-content: space-between;
                    margin-top: 10px;
                }

                .date {
                    display: flex;
                    flex-wrap: wrap;
                }

                .date>div {
                    width: calc(600px / 8);
                    height: 35px;
                    box-sizing: border-box;
                    line-height: 35px;
                    margin: 20px 5px 0;
                    text-align: center;

                }
            </style>
        </head>
        <body>
             <div class="wrap">
                        <div class="head">
                            <div class="nowDate"></div>
                            <div><select name="" id="year"></select>年</div>
                            <div><select name="" id="month"></select>月</div>
                            <button id="btn">返回今天</button>
                            <div class="switch">
                                <button id="pre">&lt;</button>
                                <button id="next">&gt;</button>
                            </div>
                        </div>
                        <!-- 星期 -->
                        <div class="title"></div>
                        <!-- 日期 -->
                        <div class="date"></div>
                    </div>
        </body>
        <script>
            main()
            function main(){
                  //获取date的父级盒子
                  var oDate = document.querySelector('.date')
                //获取年月的父盒子
                var oYear = document.getElementById('year');
                var oMonth = document.getElementById('month');
                var oTitle = document.querySelector('.title');
                console.log(oTitle)
                var oNowDate = document.querySelector('.nowDate');
                var weekArr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
                //获取当前实时年月日
                var now = new Date();
                //获取当前日期中的年
                var a = now.getFullYear();
                console.log(a);
                //获取当前的月份 只能为0-11，所以后面+1
                var b = now.getMonth() + 1;
                //获取当前的日
                var c = now.getDate();
                console.log(a, b, c);
                initView();

                function initView() {
                    //1.循环创建出星期
                    for (var i = 0; i < 7; i++) {
                        var oWeek = document.createElement('div');
                        oWeek.className = 'week';
                        oWeek.innerHTML = weekArr[i];
                        oTitle.appendChild(oWeek);
                    }
                    //2.循环创建年份
                    for (var year = 1990; year <= 3000; year++) {
                        createOption(year, year, oYear);
                    }
                    for (var month = 1; month <= 12; month++) {
                        createOption(month, month, oMonth);
                    }
                    //3.显示在左上角nowDate中
                    oNowDate.innerHTML = a + "年" + b + "月";
                    //显示在年月选项卡中
                    showSelect(a, b);
                    //4.处理下面的日期
                    showDates();
                    //5.当选项卡改变的时候
                    change();
                    //6.切换日期
                    preNextClick();
                    //7.返回今天
                    btn.onclick=function(){
                        location.reload();//一键刷新
                    }

                }
                //6.切换日期函数
                function preNextClick(){
                    //先给pre绑定点击事件
                    pre.onclick = function(){
                        //先获取选项卡中的value值
                        var yearNow = oYear.value;
                        var monthNow = oMonth.value;
                        monthNow--;
                        if(monthNow == 0){
                            monthNow = 12;
                            yearNow--
                        }
                        //调用显示日期的函数
                        showDates();
                        showSelect(yearNow, monthNow);
                        //改变左上角日期
                        oNowDate.innerHTML = yearNow + '年' + monthNow +'月'

                    }
                         //先给next绑定点击事件
                         next.onclick = function(){
                        //先获取选项卡中的value值
                        var yearNow = oYear.value;
                        var monthNow = oMonth.value;
                        monthNow++;
                        if(monthNow == 13){
                            monthNow = 1;
                            yearNow++
                        }
                        //调用显示日期的函数
                        showDates();
                        showSelect(yearNow, monthNow);
                        //改变左上角日期
                        oNowDate.innerHTML = yearNow + '年' + monthNow +'月'

                    }
                }
                //5.当选项卡改变的时候函数
                function change(){
                    //当年改变的时候
                    oYear.onchange = function(){
                        showDates();
                        //改变左上角的年月
                        oNowDate.innerHTML = `${oYear.value}年${oMonth.value}`
                    }
                    oMonth.onchange =function(){
                        showDates();
                           //改变左上角的年月
                           oNowDate.innerHTML = `${oYear.value}年${oMonth.value}`
                    }
                }


                //获取当前月份的1号是星期几
                function getDays(year,month){
                    var d = new Date(year,month,1).getDay();
                    return d;
                }
                //获取当前月份有几天
                function getDatesOfMonth(year,month){
                    var d = new Date(year,month + 1,0);// 创建日期对象
                   return  d.getDate()//获取日期的天数
                }



                //根据当前选项卡中的值来显示日期
                function showDates(){
                    oDate.innerHTML = '';
                    var year  = oYear.value;
                    var month = oMonth.value - 1;
                    //创建没有日期的盒子
                    for(var i = 0;i <getDays(year,month);i++ ){
                        var oDiv = document.createElement('div');
                        oDiv.innerHTML = '';
                        oDate.appendChild(oDiv)
                    }
                    //创建有日期的盒子
                    for(var i = 1;i <= getDatesOfMonth(year,month,);i++){
                        var oDiv = document.createElement('div');
                        oDiv.innerHTML = i;
                        oDiv.style.background = 'red';
                        //让实时日期高亮
                        if(oDiv.innerHTML == c){
                            oDiv.style.border = `2px solid yellow`;
                        }
                        oDate.appendChild(oDiv)

                    }
                }
                //显示在年月的选项卡中的函数
                function showSelect(year, month) {
                    oYear.value = year;
                    oMonth.value = month;
                }


                //创建option的函数
                function createOption(text, value, parent) {
                    var option = document.createElement('option') //
                    option.innerHTML = text;
                    option.value = value;
                    parent.appendChild(option);
                }
            }
        /*

        1.完成基本布局
        2.js部分
            1.循环创建出星期
            2.处理年月列表表单
                1.获取年月的父盒子
                2.循环创建年份  月份
        3.获取当前的日期
            1.显示在左上角的newDate中
            2.显示在年月的选项卡中
        4.处理下面的日期
            1.循环创建出当前选项卡中的日期
                1.先创建出当前选项卡中的日期
                    1.先创建空盒子
                    2.再创建出有日期的盒子
                    3让实时日期高亮
        5.当选项卡改变时
            1 调用显示日期的函数
            2 改变左上角的年月
        6.处理上下切换
            1. 绑定点击事件
            2.获取当前选项卡中的value值
            3.改变选项卡
            4.改变下面的日期
            5.改变左上角的年月
        7.处理返回今天

        */
        </script>
        </html>
```

# my date

```
import { LightningElement, track, wire } from "lwc";
import GetHolidays from "@salesforce/apex/SFDX_Holidays.getHolidays";

export default class sfdxDate extends LightningElement {
    // d = new Date();
    // year = this.d.getFullYear();

    holidays;
    error;
    @wire(GetHolidays)
    wiredHolidays({ data, error }) {
        if (data) {
            this.holidays = data;
            this.error = undefined;
        } else if (error) {
            this.error = error;
            this.holidays = undefined;
        }
    }
    //获取当前月份的1号是星期几
    getDays = function (year, month) {
        var d = new Date(year, month - 1, 1).getDay();
        return d;
    };
    //获取当前月份有几天
    getDatesOfMonth = function (year, month) {
        var d = new Date(year, month, 0); // 创建日期对象
        return d.getDate(); //获取日期的天数
    };

    showDates = function () {
        let d1 = this.getDays(2022, 10);
        let d = this.getDays(this.year, this.month);
        let days = this.getDatesOfMonth(this.year, this.month);
        // let Dates = Array.apply(null, { length: 42 });
        let Dates = Array(42).fill(0);
        console.log("year:" + this.year, "month:" + this.month);
        console.log(Dates[11], "3333");
        console.log(d1, d, days, "5555");
        for (let index = 6; index < 32; index++) {
            Dates[index] = index - 6 + 1;
        }
        console.log(Dates[11], "4444");
        return Dates;
    };
    @track
    // Dates = this.showDates.Dates;
    Dates = this.showDates();
    testDay = 12;

    years = [];
    initView = function () {
        // let oYear0 = this.template.querySelector(".select");
        // let oYear = this.template.getElementsByClassName("slds-select");
        // let oYear1 = this.template.querySelectorAll("select");
        // console.log(oYear0, oYear1);
        //console.log(oYear.Type, oYear1.Type);
        //2.循环创建年份
        for (let year = 1990; year <= 3000; year++) {
            //oYear.appendChild(new Option(year,year));
            // this.createOption(year, year, oYear);
            this.years.push(year);
            // oYear.options[year] = new Option(year, year);
            // oYear.appendChild(new Option(year, year));
        }
        this.showDates();
    };
    main = function () {
        //获取当前实时年月日
        let now = new Date();

        //获取当前日期中的年
        let year = now.getFullYear();

        //获取当前的月份 只能为0-11，所以后面+1
        let month = now.getMonth() + 1;
        //获取当前的日
        let day = now.getDate();

        console.log(year);
        console.log(year, month, day);

        this.initView();
    };
    @track
    year = this.main.year;

    @track
    month = this.main.month;

    connectedCallback() {
        this.main();
    }
```

# Test class practice

## Mock [Testing HTTP Callouts by Implementing the HttpCalloutMock Interface](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_classes_restful_http_testing_httpcalloutmock.htm)

Implementing Class

```
/**
 * CGC_SI3PricingWS_Test
 *
 * @author Kai Tian
 * @date 10/25/2022
 * @description test class for CGC_SI3PricingWS
 */
public with sharing class CGC_SI3PricingWS_Test implements HttpCalloutMock{
    /**
     * @description respond description
     * @param  req req description
     * @return     return description
     */
    public HttpResponse respond(HttpRequest req) {

        CGC_SI3PricingWS.SI3PricingModel objSI3PM = new CGC_SI3PricingWS.SI3PricingModel();
        CGC_SI3PricingWS.SI3ProductPricing objSI3PP01 = new CGC_SI3PricingWS.SI3ProductPricing();
        objSI3PP01.CompanyId=01;
        objSI3PP01.ClientId='01';
        objSI3PP01.Sku='01';
        objSI3PP01.InitialPrice=10;
        objSI3PP01.Taxes=0.8;
        objSI3PP01.OninvoiceDiscounts=0.8;
        objSI3PP01.OffinvoiceDiscounts=0.9;
        objSI3PP01.Sfp=10;
        objSI3PP01.Promochain=10;
        objSI3PP01.MaxEuroBottle=10;
        objSI3PP01.MaxEuroBottle_Promochain=10;
        objSI3PP01.MaxEuroBottle_SFP=10;

        CGC_SI3PricingWS.SI3ProductPricing objSI3PP02 = new CGC_SI3PricingWS.SI3ProductPricing();
        objSI3PP01.CompanyId=02;
        objSI3PP01.ClientId='02';
        objSI3PP01.Sku='02';
        objSI3PP01.InitialPrice=10;
        objSI3PP01.Taxes=0.8;
        objSI3PP01.OninvoiceDiscounts=0.8;
        objSI3PP01.OffinvoiceDiscounts=0.9;
        objSI3PP01.Sfp=10;
        objSI3PP01.Promochain=10;
        objSI3PP01.MaxEuroBottle=10;
        objSI3PP01.MaxEuroBottle_Promochain=10;
        objSI3PP01.MaxEuroBottle_SFP=10;

        CGC_SI3PricingWS.SI3ProductPricing objSI3PP03 = new CGC_SI3PricingWS.SI3ProductPricing();
        objSI3PP01.CompanyId=03;
        objSI3PP01.ClientId='03';
        objSI3PP01.Sku='03';
        objSI3PP01.InitialPrice=10;
        objSI3PP01.Taxes=0.8;
        objSI3PP01.OninvoiceDiscounts=0.8;
        objSI3PP01.OffinvoiceDiscounts=0.9;
        objSI3PP01.Sfp=10;
        objSI3PP01.Promochain=10;
        objSI3PP01.MaxEuroBottle=10;
        objSI3PP01.MaxEuroBottle_Promochain=10;
        objSI3PP01.MaxEuroBottle_SFP=10;

        objSI3PM.data.add(objSI3PP01);
        objSI3PM.data.add(objSI3PP02);
        objSI3PM.data.add(objSI3PP03);
        String strBody= JSON.serialize(objSI3PM);

        HttpResponse objRes = new HttpResponse();
        objRes.setHeader('Content-Type', 'application/json');
        objRes.setBody(strBody);
        objRes.setStatusCode(200);
        return objRes;

    }



}
```

TestClass

```
@isTest
private class CalloutClassTest {
     @isTest static void testCallout() {
        // Set mock callout class
        Test.setMock(HttpCalloutMock.class, new MockHttpResponseGenerator());

        // Call method to test.
        // This causes a fake response to be sent
        // from the class that implements HttpCalloutMock.
        HttpResponse res = CalloutClass.getInfoFromExternalService();

        // Verify response received contains fake values
        String contentType = res.getHeader('Content-Type');
        System.assert(contentType == 'application/json');
        String actualValue = res.getBody();
        String expectedValue = '{"example":"test"}';
        System.assertEquals(actualValue, expectedValue);
        System.assertEquals(200, res.getStatusCode());
    }
}
```

## [JSON serialize](https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_class_System_Json.htm#apex_System_Json_serialize)

```
String strBody = JSON.serialize(objModel);
```
# recovery computer 
dowload windows IOS ([use MSDN](https://msdn.itellyou.cn/))xunlei dowload it 
open the file with Windows Explorer and excute with admin user right click setup.exe .

# disk partition
Right-click my computer, find the disk partition, and operate

# view Windows activation key
```
wmic path softwarelicensingservice get OA3xOriginalProductKey
```
# [Map in JavaScript ](https://www.sfdcblogs.com/post/useful-javascript-s-methods-in-lwc-and-lightning-component-part-ii)

# [ Salesforce Apex Guide ](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_dev_guide.htm)

# [Pyramid Principle](https://www.youtube.com/watch?v=OtPbu2mje2c)

Overall score overall structure

# 2022/12/08
leetcode 每日一题完成
买了华为的云服务器 准备先来搭建博客（哔哩哔哩上的鱼皮） 使用宝塔 对于宝塔的端口（需要在安全组中开放8888、888、80、443、20和21端口）
VPN的使用 飞鸟云 [防失联链接]：(https://feiniaoyun.gitbook.io/fabu/)
clash for windows 工具使用

# maven的安装和配置
Windows下载zip文件解压
在conf文件中配置仓库以及本地仓库的存储位置

# [spring & spring boot](https://spring.io/)
开始一个web项目start.spring.io
spring 的核心IoC 和 Aop
IoC：inversion of control 控制反转 采用Dependencies Injection 依赖注入的思想
不需要程序员自己去手动的去实例化bean，程序员只需要通过注解的方式提供要实例化的bean和相应的配置就可以去让spring容器去实例化。
2022-12-12 学到的注解
```

//配置类，一般是程序的入口用这个注解，一般的配置类使用Configuration
SpringBootApplication
Configuration

//对于要实例化的对象的配置
Component("实例化的实例名,这四个都一样") //如果类在控制、业务以及数据库都有关，可以用Component注解
        //后面的三个都是依赖于Component的，四者其实并没有本质的区别
Controller //用于控制
Service //关于业务
Repository //用于操作数据库

//当一个接口有两个实现类的时候使用Primary的注解生命spring实现返回哪个bean的实例
Primary

//生命bean的初始化方法，和构造方法不同，构造方法会先执行
PostConstruct

//声明bean的销毁方法。在销毁实例前执行
PreDestroy

//实例化单例：singleton还是多例：prototype
Scope("singleton") 

//对于第三方的类的实例化
Bean
public 想要实例化的类名 方法名（也就是spring实例化类后的实例名）{return new 想要实例化的类名()}

//自动装配，将实例化的类赋值到需要的地方
Autowired
Qulifier("实例化后的实例名")

/*@ContextConfiguration这个注解通常与@RunWith(SpringJUnit4ClassRunner.class)联合使用用来测试
当一个类添加了注解@Component,那么他就自动变成了一个bean，就不需要再Spring配置文件中显示的配置了。把这些bean收集起来通常有两种方式，Java的方式和XML的方式。当这些bean收集起来之后，当我们想要在某个测试类使用@Autowired注解来引入这些收集起来的bean时，只需要给这个测试类添加@ContextConfiguration注解来标注我们想要导入这个测试类的某些bean。*/
ContextConfiguration(Class = ...(想要收集的实例化的bean))

```
# spring MVC

其他所有的spring XXX都是基于spring的核心IoC和AOP

服务器三层架构分为表现层（Controller） 、业务层（Service） 、 数据层（Repository）
MVC是一种思想，主要体现在表现层的部分，Model View Controller
Controller将从service得到的model给view，最后view将用model处理后的view传给controller，最后再传到用户界面
![spring mvc 模式图](https://user-images.githubusercontent.com/83005912/207338154-9a92958d-760e-4b8c-96ea-6cd285fcbb71.png)

核心部件是dispatcherservlet，它会根据配置信息将路径分配到对应的controller类上，model不用程序员自己来实例

要实现动态的HTML还要借助渲染工具，最流行的是[thymeleaf](https://www.thymeleaf.org/) （由于thyme leaf是基于HTML的）
在使用时候要传入model和模板

学到的注解
```
//手动的实现
@RequestMapping("/http")
	public void http(HttpServletRequest request, HttpServletResponse response) {
		//request
		System.out.println(request.getMethod());
		System.out.println(request.getContextPath());
		Enumeration<String> names = request.getHeaderNames();
		while (names.hasMoreElements()) {
			String name = names.nextElement();
			String value = request.getHeader(name);
			System.out.println(name + ": " + value);
		}
		System.out.println(request.getParameter("code"));
		
		//response
		response.setContentType("text/html;charset=utf-8");
		response.setStatus(200);
		try (PrintWriter writer = response.getWriter()) {
			writer.write("<h1>TK网</h1>");
		} catch (IOException e) {
			throw new RuntimeException(e);
		}
		
	}
        
//对应请求路径
@RequestMapping("/alpha") //参数有path，method等
@RequestMapping(path = "/students", method = RequestMethod.GET)

//返回响应体（没有这个默认是返回HTML页面）
ResponseBody

//对应请求的参数（写在方法的参数里面）
@RequestParam(name = "current", required = false, defaultValue = "1") int current

//对应路径的参数（写在方法的参数里面）
@PathVariable(name = "id", required = true) int id

//动态HTML
	@RequestMapping(path = "/teacher", method = RequestMethod.GET)
	public ModelAndView getTeacher() {
		ModelAndView mav = new ModelAndView();
		mav.addObject("name", "张三");
		mav.addObject("age", "23");
		mav.setViewName("/demo/teacher");
		return mav;
		
	}
        //较为简单的实现，效果一样
        @RequestMapping(path = "/school", method = RequestMethod.GET)
	public String getSchool(Model model) {
		model.addAttribute("name", "北京大学");
		model.addAttribute("age", 80);
		return "/demo/teacher";
		
	}
        
//返回JSON（常用于异步）
@RequestMapping(path = "/emps", method = RequestMethod.GET)
	@ResponseBody
	public List<Map<String, Object>> getEmps() {
		List<Map<String, Object>> list = new ArrayList<>();
		
		Map<String, Object> map = new HashMap<String, Object>();
		map.put("name", "张三");
		map.put("age", 20);
		map.put("salary", 8000.00);
		list.add(map);
		
		map = new HashMap<String, Object>();
		map.put("name", "李四");
		map.put("age", 31);
		map.put("salary", 10000.00);
		list.add(map);
		
		return list;
		
		
	}
```

## 关于application.properties

设置相关类的属性的值
[常用到的一些配置](https://docs.spring.io/spring-boot/docs/2.1.1.RELEASE/reference/htmlsingle/#common-application-properties)

# 关于Mybatis

## Mybatis是什么

MyBatis是一个持久层框架，用于将Java应用程序与数据库连接。它使用SQL映射器来简化持久层代码，使用XML或注解来配置SQL语句。这样，开发人员就可以专注于业务逻辑，而不必担心复杂的数据访问代码。MyBatis还提供了一种称为动态SQL的机制，可以动态生成SQL语句，使得开发人员可以创建复杂的查询。MyBatis是一个开源框架，可以免费使用。

## Mybatis的核心机制

MyBatis的核心机制包括以下几个方面：

- SQL映射器：MyBatis使用SQL映射器将SQL语句与Java方法相关联。这样，开发人员就可以通过调用Java方法来执行SQL语句，而不必写复杂的数据访问代码。

- 动态SQL：MyBatis提供了一种称为动态SQL的机制，可以动态生成SQL语句。这使得开发人员可以创建复杂的查询，并且可以根据应用程序的需要动态地更改SQL语句。

- 数据映射器：MyBatis使用数据映射器将数据库记录与Java对象相关联。这样，开发人员就可以使用Java对象来访问数据库记录，而不必写复杂的数据访问代码。

- 会话工厂：MyBatis使用会话工厂管理数据库连接。开发人员可以通过调用会话工厂的方法来获取数据库连接，并且可以在使用完数据库连接后将其关闭。

- 缓存：MyBatis提供了一个二级缓存机制，可以提高查询性能。缓存可以缓存常用的SQL查询结果，避免重复执行SQL语句。

## Mybatis Spring比Mybatis好在哪里

Mybatis Spring是对Mybatis的一种封装，它将Mybatis整合到Spring框架中。使用Mybatis Spring可以享受Spring框架的众多优势，这些优势包括：

- Spring管理Mybatis的会话工厂：在Spring中使用Mybatis时，可以使用Spring管理Mybatis的会话工厂，从而简化代码并减少错误。

- Spring管理数据源：使用Mybatis Spring时，可以使用Spring管理数据源，从而简化代码并减少错误。

- Spring管理事务：使用Mybatis Spring时，可以使用Spring管理事务，从而简化代码并减少错误。

- 使用Spring的依赖注入：使用Mybatis Spring时，可以使用Spring的依赖注入机制，从而简化代码并减少错误。

- 使用Spring的AOP机制：使用Mybatis Spring时，可以使用Spring的AOP机制，从而在执行数据库操作时实现更复杂的功能。

总之，使用Mybatis Spring可以简化代码，减少错误，并使用Spring框架的众多优势。

## 如何使用Mybatis

- 在pom.xml文件中导入MySQL和Mybatis的依赖
```
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>8.0.31</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
```
- 在application.properties文件中配置数据库连接池和Mybatis的相关内容
```
# DataSourceProperties
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://localhost:3306/community
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.type=com.zaxxer.hikari.HikariDataSource
spring.datasource.hikari.maximum-pool-size=15
spring.datasource.hikari.minimum-idle=15
spring.datasource.hikari.minimum-idle-timeout=30000


# MybatisProperties
mybatis.mapper-locations=classpath:mapper/*.xml
mybatis.type-aliases-package=com.tk.community.entity
mybatis.configuration.map-underscore-to-camel-case=true
mybatis.configuration.use-generated-keys=true
#mybatis.configuration.default-fetch-size=100
#mybatis.configuration.default-statement-timeout=30
```

- 创建实体类

```
public class User {
	
	private int id;
	private String username;
	private String password;
	private String salt;
	
	private String email;
	private int type;
	private int status;
	private String activationCode;
	private String headerUrl;
	private Date createTime;
public int getId() {
		return id;
	}
	
	public void setId(int id) {
		this.id = id;
	}
	
	public String getUsername() {
		return username;
	}
	
	public void setUsername(String username) {
		this.username = username;
	}
	
	public String getPassword() {
		return password;
	}
	
	public void setPassword(String password) {
		this.password = password;
	}
	
	public String getSalt() {
		return salt;
	}
	
	public void setSalt(String salt) {
		this.salt = salt;
	}
	
	public String getEmail() {
		return email;
	}
	
	public void setEmail(String email) {
		this.email = email;
	}
	
	public int getType() {
		return type;
	}
	
	public void setType(int type) {
		this.type = type;
	}
	
	public int getStatus() {
		return status;
	}
	
	public void setStatus(int status) {
		this.status = status;
	}
	
	public String getActivationCode() {
		return activationCode;
	}
	
	public void setActivationCode(String activationCode) {
		this.activationCode = activationCode;
	}
	
	public String getHeaderUrl() {
		return headerUrl;
	}
	
	public void setHeaderUrl(String headerUrl) {
		this.headerUrl = headerUrl;
	}
	
	public Date getCreateTime() {
		return createTime;
	}
	
	public void setCreateTime(Date createTime) {
		this.createTime = createTime;
	}
	
	@Override
	public String toString() {
		return "User{" +
				       "id=" + id +
				       ", username='" + username + '\'' +
				       ", password='" + password + '\'' +
				       ", salt='" + salt + '\'' +
				       ", type=" + type +
				       ", status=" + status +
				       ", activationCode='" + activationCode + '\'' +
				       ", headerUrl='" + headerUrl + '\'' +
				       ", createTime=" + createTime +
				       '}';
	}
}
```

- 创建DAO（Data Access Object)

```
package com.tk.community.dao;

import com.tk.community.entity.User;
import org.apache.ibatis.annotations.Mapper;

@Mapper
public interface UserMapper {
	
	User selectById(int id);
	
	User selectByName(String username);
	
	User selectByEmail(String email);
	
	int insertUser(User user);
	
	int updateStatus(int id, int status);
	
	int updateHeader(int id,String headerUrl);
	
	int updatePassword(int id,String password);
}
```

- 在resources的mapper下创建相关的 .xml文件

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.tk.community.dao.UserMapper">

    <sql id="selectFields">id,username,password,salt,email,type,status,activation_code,header_url,create_time</sql>

    <sql id="insertFields">username,password,salt,email,type,status,activation_code,header_url,create_time</sql>

    <select id="selectById" resultType="User">
        SELECT
        <include refid="selectFields"></include>
        FROM user
        WHERE id = #{id}
    </select>

    <select id="selectByName" resultType="User">
        SELECT
        <include refid="selectFields"></include>
        FROM user
        WHERE username = #{username}
    </select>

    <select id="selectByEmail" resultType="User">
        SELECT
        <include refid="selectFields"></include>
        FROM user
        WHERE email = #{email}
    </select>


    <insert id="insertUser" parameterType="User" keyProperty="id">
        insert into user (<include refid="insertFields"></include>)
        values(#{username},#{password},#{salt},#{email},#{type},#{status},#{activationCode},#{headerUrl},#{createTime})
    </insert>


    <update id="updateStatus">
        update user set status = #{status} where id = #{id}
    </update>

    <update id="updateHeader">
        update user set header_url = #{headerUrl} where id = #{id}
    </update>

    <update id="updatePassword">
        update user set password = #{password} where id = #{id}
    </update>

</mapper>
```
- 最后是在service中调用DAO的接口

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.tk.community.dao.UserMapper">

    <sql id="selectFields">id,username,password,salt,email,type,status,activation_code,header_url,create_time</sql>

    <sql id="insertFields">username,password,salt,email,type,status,activation_code,header_url,create_time</sql>

    <select id="selectById" resultType="User">
        SELECT
        <include refid="selectFields"></include>
        FROM user
        WHERE id = #{id}
    </select>

    <select id="selectByName" resultType="User">
        SELECT
        <include refid="selectFields"></include>
        FROM user
        WHERE username = #{username}
    </select>

    <select id="selectByEmail" resultType="User">
        SELECT
        <include refid="selectFields"></include>
        FROM user
        WHERE email = #{email}
    </select>


    <insert id="insertUser" parameterType="User" keyProperty="id">
        insert into user (<include refid="insertFields"></include>)
        values(#{username},#{password},#{salt},#{email},#{type},#{status},#{activationCode},#{headerUrl},#{createTime})
    </insert>


    <update id="updateStatus">
        update user set status = #{status} where id = #{id}
    </update>

    <update id="updateHeader">
        update user set header_url = #{headerUrl} where id = #{id}
    </update>

    <update id="updatePassword">
        update user set password = #{password} where id = #{id}
    </update>

</mapper>
```

# Git版本控制

- 下载git
- 配置git
```
git config --list //显示目前所有的配置
git config --global user.name "" user.email ""//配置用户名和邮箱
```
- 上传到本地
```
//进入想要上传的项目

//初始化
git init

//将文件提交到暂存区
git add ...

//将暂存区中的文件提交到版本库中
git commit -m "信息"
```

- 上传到远程
```
//生成密钥
ssh-keygen -t rsa -C "1879783522@qq.com"

//将密钥在远程上存储

//链接远程
git remote add origin <remote repository URL>

//将本地的内容推送到远程
git push -u origin master
```

# 使用邮件Mail

- 在邮箱上开启POP3|SMTP服务
- 在pom.xml中注入依赖
```
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-mail</artifactId>
            <version>3.0.0</version>
        </dependency>
```
- 创建一个可以复用的utils类Mail（示例）
```
package com.tk.community.util;

import jakarta.mail.MessagingException;
import jakarta.mail.internet.MimeMessage;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.mail.MailSender;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.stereotype.Component;

@Component
public class MailClient {
	
	public static final Logger logger = LoggerFactory.getLogger(MailClient.class);
	
	
	@Autowired
	private JavaMailSender mailSender;
	
	@Value("${spring.mail.username}")
	private String from;
	
	public void sentMail(String to, String subject, String content) {
		try {
			MimeMessage mimeMessage = mailSender.createMimeMessage();
			MimeMessageHelper mimeMessageHelper = new MimeMessageHelper(mimeMessage);
			mimeMessageHelper.setFrom(from);
			mimeMessageHelper.setTo(to);
			mimeMessageHelper.setSubject(subject);
			mimeMessageHelper.setText(content, true);
			mailSender.send(mimeMessageHelper.getMimeMessage());
		} catch (MessagingException e) {
			logger.error("发送邮件失败：" + e.getMessage());
		}
		
	}
}
```
- 使用MialClient
```
//测试类
package com.tk.community.util;

import jakarta.mail.MessagingException;
import jakarta.mail.internet.MimeMessage;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.mail.MailSender;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.stereotype.Component;

@Component
public class MailClient {
	
	public static final Logger logger = LoggerFactory.getLogger(MailClient.class);
	
	
	@Autowired
	private JavaMailSender mailSender;
	
	@Value("${spring.mail.username}")
	private String from;
	
	public void sentMail(String to, String subject, String content) {
		try {
			MimeMessage mimeMessage = mailSender.createMimeMessage();
			MimeMessageHelper mimeMessageHelper = new MimeMessageHelper(mimeMessage);
			mimeMessageHelper.setFrom(from);
			mimeMessageHelper.setTo(to);
			mimeMessageHelper.setSubject(subject);
			mimeMessageHelper.setText(content, true);
			mailSender.send(mimeMessageHelper.getMimeMessage());
		} catch (MessagingException e) {
			logger.error("发送邮件失败：" + e.getMessage());
		}
		
	}
}
//HTML模板（与thymeleaf相结合）
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Demo</title>
</head>
<body>
    <div>Welcome to community <div style="color:red;" th:utext="${username}"></div></div>
</body>
</html>
```

# 注册功能

- 注册页面

```
    @RequestMapping(path = "/register",method = RequestMethod.GET)
	public String getRegisterPage(){
		return "site/register";
	}
```

- userService中的注册判断

```
    public Map<String, Object> register(User user) {
		Map<String, Object> map = new HashMap<>();
		
		//空值处理
		if (user == null) {
			throw new IllegalArgumentException("参数不能为空！");
		}
		if (StringUtils.isBlank(user.getUsername())) {
			map.put("usernameMsg", "账号不能为空！");
		}
		if (StringUtils.isBlank(user.getPassword())) {
			map.put("passwordMsg", "密码不能为空！");
		}
		if (StringUtils.isBlank(user.getEmail())) {
			map.put("emailMsg", "邮箱不能为空！");
		}
		
		//验证账号
		User u = userMapper.selectByName(user.getUsername());
		if (u != null) {
			map.put("usernameMsg", "该账号名已存在！");
			return map;
		}
		
		//验证邮箱
		u = userMapper.selectByEmail(user.getEmail());
		if (u != null) {
			map.put("emailMsg", "该邮箱已被注册！");
			return map;
		}
		
		//注册用户
		user.setSalt(CommunityUtil.generateUUID().substring(0, 5));
		user.setPassword(CommunityUtil.md5(user.getPassword() + user.getSalt()));
		user.setType(0);
		user.setStatus(0);
		user.setActivationCode(CommunityUtil.generateUUID());
		user.setHeaderUrl(String.format("http://images.nowcoder.com/head/%dt.png", new Random().nextInt(1000)));
		user.setCreateTime(new Date());
		userMapper.insertUser(user);
		
		//激活邮件
		Context context = new Context();
		context.setVariable("email", user.getEmail());
		String url = domain + contextPath + "/activation" + user.getId() + "/" + user.getActivationCode();
		context.setVariable("url", url);
		String content = templateEngine.process("/mail/activation", context);
		mailClient.sentMail(user.getEmail(), "激活账号", content);
		
		return map;
		
	}
```

- 对于registerController

```
    @RequestMapping(path = "/register",method = RequestMethod.POST)
	public String register(Model model, User user){
		Map<String, Object> map = userService.register(user);
		if (map == null || map.isEmpty()) {
			model.addAttribute("msg","注册成功，我们已经向您的邮箱发送了一封激活邮件，请尽快激活！");
			model.addAttribute("target","index");
			return "/site/operate-result";
			
		}else {
			model.addAttribute("usernameMsg",map.get("usernameMsg"));
			model.addAttribute("passwordMsg",map.get("passwordMsg"));
			model.addAttribute("emailMsg",map.get("emailMsg"));
			return "/site/register";
			
		}
		
	}
```

- 对于register页面的逻辑

```
    <!-- 内容 -->
		<div class="main">
			<div class="container pl-5 pr-5 pt-3 pb-3 mt-3 mb-3">
				<h3 class="text-center text-info border-bottom pb-3">注&nbsp;&nbsp;册</h3>
				<form class="mt-5" method="post" th:action="@{/register}">
					<div class="form-group row">
						<label for="username" class="col-sm-2 col-form-label text-right">账号:</label>
						<div class="col-sm-10">
							<input type="text"
								   th:class="|form-control ${usernameMsg!=null?'is-invalid':''}|"
								   th:value="${user!=null?user.username:''}"
								   id="username" name="username" placeholder="请输入您的账号!" required>
							<div class="invalid-feedback" th:text="${usernameMsg}">
								该账号已存在!
							</div>
						</div>
					</div>
					<div class="form-group row mt-4">
						<label for="password" class="col-sm-2 col-form-label text-right">密码:</label>
						<div class="col-sm-10">
							<input type="password"
								   th:class="|form-control ${passwordMsg!=null?'is-invalid':''}|"
								   th:value="${user!=null?user.password:''}"
								   id="password" name="password" placeholder="请输入您的密码!" required>
							<div class="invalid-feedback" th:text="${passwordMsg}">
								密码长度不能小于8位!
							</div>							
						</div>
					</div>
					<div class="form-group row mt-4">
						<label for="confirm-password" class="col-sm-2 col-form-label text-right">确认密码:</label>
						<div class="col-sm-10">
							<input type="password" class="form-control"
								   th:value="${user!=null?user.password:''}"
								   id="confirm-password" placeholder="请再次输入密码!" required>
							<div class="invalid-feedback">
								两次输入的密码不一致!
							</div>
						</div>
					</div>
					<div class="form-group row">
						<label for="email" class="col-sm-2 col-form-label text-right">邮箱:</label>
						<div class="col-sm-10">
							<input type="email"
								   th:class="|form-control ${emailMsg!=null?'is-invalid':''}|"
								   th:value="${user!=null?user.email:''}"
								   id="email" name="email" placeholder="请输入您的邮箱!" required>
							<div class="invalid-feedback" th:text="${emailMsg}">
								该邮箱已注册!
							</div>
						</div>
					</div>
					<div class="form-group row mt-4">
						<div class="col-sm-2"></div>
						<div class="col-sm-10 text-center">
							<button type="submit" class="btn btn-info text-white form-control">立即注册</button>
						</div>
					</div>
				</form>				
			</div>
		</div>
```

# 验证码生成
- 引入kaptcha的依赖
```
        <dependency>
            <groupId>com.github.penggle</groupId>
            <artifactId>kaptcha</artifactId>
            <version>2.3.2</version>
        </dependency>
```
- 对kaptcha进行配置
```
package com.tk.community.config;

import com.google.code.kaptcha.Producer;
import com.google.code.kaptcha.impl.DefaultKaptcha;
import com.google.code.kaptcha.util.Config;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.util.Properties;

@Configuration
    public class KaptchaConfig {
	
	@Bean
	public Producer kaptchaProducer() {
		
		Properties properties = new Properties();
		properties.setProperty("kaptcha.image.width", "100");
		properties.setProperty("kaptcha.image.height", "40");
		properties.setProperty("kaptcha.textproducer.font.size", "32");
		properties.setProperty("kaptcha.textproducer.font.color", "0,0,0");
		properties.setProperty("kaptcha.textproducer.char.string", "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ");
		properties.setProperty("kaptcha.textproducer.char.length", "4");
		properties.setProperty("kaptcha.noise.impl", "com.google.code.kaptcha.impl.NoNoise");
		
		DefaultKaptcha defaultKaptcha = new DefaultKaptcha();
		Config config = new Config(properties);
		defaultKaptcha.setConfig(config);
		return defaultKaptcha;
	}
}
```
- 进行使用
```
    @RequestMapping(path = "/kaptcha", method = RequestMethod.GET)
	public void getKaptcha(HttpServletResponse response, HttpSession session) {
		//生成验证码
		String text = kaptchaProducer.createText();
		BufferedImage image = kaptchaProducer.createImage(text);
		
		//将验证码存入session
		session.setAttribute("kaptcha", text);
		
		//将图片输出给浏览器
		response.setContentType("image/png");
		try {
			ServletOutputStream stream = response.getOutputStream();
			boolean b = ImageIO.write(image, "png", stream);
		} catch (IOException e) {
			logger.error("响应验证码失败：" + e.getMessage());
		}
		
	}

    //html:
    <div class="col-sm-4">
        <img th:src="@{/kaptcha}" id="kaptcha" style="width:100px;height:40px;" class="mr-2"/>
        <a href="javascript:refresh_kaptcha();" class="font-size-12 align-bottom">刷新验证码</a>
    </div>
    //js:使用jQuery：
    <script src="https://code.jquery.com/jquery-3.3.1.min.js" crossorigin="anonymous"></script>
    <script>
    function refresh_kaptcha(){
        var path = CONTEXT_PATH + "/kaptcha?p=" + Math.random();//CONTEXT_PATH:项目的路径
        $("#kaptcha").attr("src",path);
    }

</script>    
```

# Cookie & Session

Cookies and sessions are mechanisms that allow a website to store data on a user's device and retrieve it later. They are commonly used to store user preferences, track user activity, and provide a more personalized user experience.

Cookies are small pieces of data that are stored on a user's device by a web browser. They are typically used to store user preferences and other information that needs to be persisted across multiple requests or visits to a website. Cookies are stored on the user's device and are sent back to the server with each request, allowing the server to access and use the stored data.

Sessions, on the other hand, are used to store data on the server side. When a user visits a website, the server creates a unique session ID and stores the session data associated with that ID. The session ID is then typically stored in a cookie on the user's device, allowing the server to associate the session data with the user's requests.

There are a few key differences between cookies and sessions:

Storage location: Cookies are stored on the user's device, while sessions are stored on the server.

Persistence: Cookies are persisted across multiple visits to a website, while sessions are typically only active for the duration of a single visit.

Size: Cookies have a size limit of 4KB, while sessions can store much larger amounts of data.

Security: Cookies are sent with every request, which means they can be accessed by anyone with access to the user's device. Sessions, on the other hand, are stored on the server and are generally more secure.

Use cases: Cookies are commonly used to store user preferences, while sessions are typically used to store temporary data that is needed during a single visit to a website.

In general, cookies are useful for storing small amounts of data that needs to be persisted across multiple visits to a website, while sessions are better suited for storing larger amounts of temporary data that is only needed during a single visit.

Cookie 和会话是允许网站在用户设备上存储数据并在以后检索的机制。它们通常用于存储用户偏好、跟踪用户活动并提供更加个性化的用户体验。

Cookie 是网络浏览器存储在用户设备上的小块数据。它们通常用于存储用户偏好和其他需要在多次请求或访问网站时保留的信息。 Cookie 存储在用户的设备上，并随每个请求发送回服务器，允许服务器访问和使用存储的数据。

另一方面，会话用于在服务器端存储数据。当用户访问网站时，服务器会创建一个唯一的会话 ID 并存储与该 ID 关联的会话数据。然后会话 ID 通常存储在用户设备上的 cookie 中，允许服务器将会话数据与用户的请求相关联。

Cookie 和会话之间存在一些主要区别：

存储位置：Cookies存储在用户的设备上，而session则存储在服务器上。

持久性：Cookie 在网站的多次访问中持续存在，而会话通常仅在单次访问期间处于活动状态。

大小：Cookie 的大小限制为 4KB，而会话可以存储更多的数据。

安全性：每次请求都会发送 Cookie，这意味着任何有权访问用户设备的人都可以访问它们。另一方面，会话存储在服务器上，通常更安全。

用例：Cookie 通常用于存储用户偏好，而会话通常用于存储单次访问网站期间所需的临时数据。

通常，cookie 可用于存储需要在多次访问网站时保留的少量数据，而会话更适合存储仅在单次访问期间需要的大量临时数据。

## cookie的使用(spring中)
```
    @RequestMapping(path = "/cookie/set", method = RequestMethod.GET)
	@ResponseBody
	public String setCookie(HttpServletResponse response) {
		Cookie cookie = new Cookie("code", CommunityUtil.generateUUID());
		cookie.setPath("/community/alpha");
		cookie.setMaxAge(600);
		response.addCookie(cookie);
		return "set cookie";
	}
	
	@RequestMapping(path = "/cookie/get", method = RequestMethod.GET)
	@ResponseBody
	public String getCookie(@CookieValue("code") String code) {
		return code;
	}
```
## session的使用
```
    @RequestMapping(path = "/session/set", method = RequestMethod.GET)
	@ResponseBody
	public String setSession(HttpSession session) {
		session.setAttribute("id", 123);
		session.setAttribute("name", "test");
		return "set session";
	}
	
	@RequestMapping(path = "/session/get", method = RequestMethod.GET)
	@ResponseBody
	public String getSession(HttpSession session) {
		Object id = session.getAttribute("id");
		Object name = session.getAttribute("name");
		System.out.println("id:" + id + "name:" + name);
		return "get session";
	}
```

# No primary or single unique constructor found for interface javax.servlet.http.HttpServletResponse问题解决

将javax.servlet.http.HttpServletResponse导入包改为jakarta.servlet.http.HttpServletResponse;

# 登录login的实现

- 创建一个entity类，LoginTicket用于用户登录凭证表
```
package com.tk.community.entity;

import java.util.Date;

public class LoginTicket {
	
	private int id;
	private int userId;
	private String ticket;
	private int status;
	private Date expired;
	
	public int getId() {
		return id;
	}
	
	public void setId(int id) {
		this.id = id;
	}
	
	public int getUserId() {
		return userId;
	}
	
	public void setUserId(int userId) {
		this.userId = userId;
	}
	
	public String getTicket() {
		return ticket;
	}
	
	public void setTicket(String ticket) {
		this.ticket = ticket;
	}
	
	public int getStatus() {
		return status;
	}
	
	public void setStatus(int status) {
		this.status = status;
	}
	
	public Date getExpired() {
		return expired;
	}
	
	public void setExpired(Date expired) {
		this.expired = expired;
	}
	
	@Override
	public String toString() {
		return "LoginTicket{" +
				       "id=" + id +
				       ", userId=" + userId +
				       ", ticket='" + ticket + '\'' +
				       ", status=" + status +
				       ", expired=" + expired +
				       '}';
	}
}
```

- 在数据库层：创建DAO
```
package com.tk.community.dao;

import com.tk.community.entity.LoginTicket;
import org.apache.ibatis.annotations.*;

@Mapper
public interface LoginTicketMapper {
	@Insert({
			"insert into login_ticket(user_id,ticket,status,expired) ",
			"values(#{userId},#{ticket},#{status},#{expired})"
	})
	@Options(useGeneratedKeys = true,keyProperty = "id")
	int insertLoginTicket(LoginTicket loginTicket);
	@Select({
					"select id,user_id,ticket,status,expired ",
					"from login_ticket where ticket=#{ticket}"
	})
	LoginTicket selectByTicket(String ticket);
    //实例在注解中如何使用if，所加内容无意义
	@Update({
					"<script>",
					"update login_ticket set status=#{status} ",
					"where ticket=#{ticket}",
					"<if test=\"ticket!=null\"> ",
					"and 1=1",
					"</if>",
					"</script>"
	})
	int updateStatus(String ticket,int status);
}
```
- 在业务层：
```
    public Map<String, Object> login(String username, String password, long expiredSeconds) {
		Map<String, Object> map = new HashMap<>();
		
		//空值处理
		if (StringUtils.isBlank(username)) {
			map.put("usernameMsg", "账号不能为空！");
			return map;
		}
		if (StringUtils.isBlank(password)) {
			map.put("passwordMsg", "密码不能为空！");
			return map;
		}
		
		//验证账号
		User user = userMapper.selectByName(username);
		if (user == null) {
			map.put("usernameMsg", "账号不存在");
			return map;
		}
		
		//验证状态
		if (user.getStatus() == 0) {
			map.put("usernameMsg", "账号未激活");
		}
		
		//验证密码
		password = CommunityUtil.md5(password + user.getSalt());
		assert password != null;
		if (!password.equals(user.getPassword())) {
			map.put("passwordMsg", "密码错误");
			return map;
		}
		
		LoginTicket loginTicket = new LoginTicket();
		loginTicket.setUserId(user.getId());
		loginTicket.setTicket(CommunityUtil.generateUUID());
		loginTicket.setStatus(0);
		loginTicket.setExpired(new Date(System.currentTimeMillis() + expiredSeconds * 1000));
		map.put("ticket",loginTicket.getTicket());
		loginTicketMapper.insertLoginTicket(loginTicket);
		
		return map;
	}
```
- 在控制层：
```
    @RequestMapping(path = "/login", method = RequestMethod.POST)
	public String login(String username, String password, String code, boolean rememberme,
	                    Model model, HttpSession session, HttpServletResponse response) {
		// 检查验证码
		String kaptcha = (String) session.getAttribute("kaptcha");
		
		if (StringUtils.isBlank(kaptcha) || StringUtils.isBlank(code) || !kaptcha.equalsIgnoreCase(code)) {
			model.addAttribute("codeMsg", "验证码不正确!");
			return "/site/login";
		}
		
		// 检查账号,密码
		int expiredSeconds = rememberme ? REMEMBER_EXPIRED_SECONDS : DEFAULT_EXPIRED_SECONDS;
		Map<String, Object> map = userService.login(username, password, expiredSeconds);
		if (map.containsKey("ticket")) {
			Cookie cookie = new Cookie("ticket", map.get("ticket").toString());
			cookie.setPath(contextPath);
			cookie.setMaxAge(expiredSeconds);
			response.addCookie(cookie);
			return "redirect:/index";
		} else {
			model.addAttribute("usernameMsg", map.get("usernameMsg"));
			model.addAttribute("passwordMsg", map.get("passwordMsg"));
			return "/site/login";
		}
	}
```
- thymeleaf模板
```
<!doctype html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="icon" href="https://static.nowcoder.com/images/logo_87_87.png"/>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
          crossorigin="anonymous">
    <link rel="stylesheet" th:href="@{/css/global.css}"/>
    <link rel="stylesheet" th:href="@{/css/login.css}"/>
    <title>牛客网-登录</title>
</head>
<body>
<div class="nk-container">
    <!-- 头部 -->
    <header class="bg-dark sticky-top" th:replace="~{index::header}">
        <div class="container">
            <!-- 导航 -->
            <nav class="navbar navbar-expand-lg navbar-dark">
                <!-- logo -->
                <a class="navbar-brand" href="#"></a>
                <button class="navbar-toggler" type="button" data-toggle="collapse"
                        data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
                        aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <!-- 功能 -->
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav mr-auto">
                        <li class="nav-item ml-3 btn-group-vertical">
                            <a class="nav-link" href="../index.html">首页</a>
                        </li>
                        <li class="nav-item ml-3 btn-group-vertical">
                            <a class="nav-link position-relative" href="letter.html">消息<span
                                    class="badge badge-danger">12</span></a>
                        </li>
                        <li class="nav-item ml-3 btn-group-vertical">
                            <a class="nav-link" href="register.html">注册</a>
                        </li>
                        <li class="nav-item ml-3 btn-group-vertical">
                            <a class="nav-link" href="login.html">登录</a>
                        </li>
                        <li class="nav-item ml-3 btn-group-vertical dropdown">
                            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button"
                               data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                                <img src="http://images.nowcoder.com/head/1t.png" class="rounded-circle"
                                     style="width:30px;"/>
                            </a>
                            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                                <a class="dropdown-item text-center" href="profile.html">个人主页</a>
                                <a class="dropdown-item text-center" href="setting.html">账号设置</a>
                                <a class="dropdown-item text-center" href="login.html">退出登录</a>
                                <div class="dropdown-divider"></div>
                                <span class="dropdown-item text-center text-secondary">nowcoder</span>
                            </div>
                        </li>
                    </ul>
                    <!-- 搜索 -->
                    <form class="form-inline my-2 my-lg-0" action="search.html">
                        <input class="form-control mr-sm-2" type="search" aria-label="Search"/>
                        <button class="btn btn-outline-light my-2 my-sm-0" type="submit">搜索</button>
                    </form>
                </div>
            </nav>
        </div>
    </header>

    <!-- 内容 -->
    <div class="main">
        <div class="container pl-5 pr-5 pt-3 pb-3 mt-3 mb-3">
            <h3 class="text-center text-info border-bottom pb-3">登&nbsp;&nbsp;录</h3>
            <form class="mt-5" method="post" th:action="@{/login}">
                <div class="form-group row">
                    <label for="username" class="col-sm-2 col-form-label text-right">账号:</label>
                    <div class="col-sm-10">
                        <input type="text" th:class="|form-control ${usernameMsg!=null?'is-invalid':''}|"
                               th:value="${param.username}"
                               name="username" id="username" placeholder="请输入您的账号!"
                               required>
                        <div class="invalid-feedback" th:text="${usernameMsg}">
                            该账号不存在!
                        </div>
                    </div>
                </div>
                <div class="form-group row mt-4">
                    <label for="password" class="col-sm-2 col-form-label text-right">密码:</label>
                    <div class="col-sm-10">
                        <input type="password" th:class="|form-control ${passwordMsg!=null?'is-invalid':''}|"
                               th:value="${param.password}"
                               name="password" id="password"
                               placeholder="请输入您的密码!" required>
                        <div class="invalid-feedback" th:text="${passwordMsg}">
                            密码长度不能小于8位!
                        </div>
                    </div>
                </div>
                <div class="form-group row mt-4">
                    <label for="verifycode" class="col-sm-2 col-form-label text-right">验证码:</label>
                    <div class="col-sm-6">
                        <input type="text" th:class="|form-control ${codeMsg!=null?'is-invalid':''}|"
                               name="code" id="verifycode" placeholder="请输入验证码!">
                        <div class="invalid-feedback" th:text="${codeMsg}">
                            验证码不正确!
                        </div>
                    </div>
                    <div class="col-sm-4">
                        <img th:src="@{/kaptcha}" id="kaptcha" style="width:100px;height:40px;" class="mr-2"/>
                        <a href="javascript:refresh_kaptcha();" class="font-size-12 align-bottom">刷新验证码</a>
                    </div>
                </div>
                <div class="form-group row mt-4">
                    <div class="col-sm-2"></div>
                    <div class="col-sm-10">
                        <input type="checkbox" id="remember-me" name="rememberme" th:checked="${param.rememberme}">
                        <label class="form-check-label" for="remember-me">记住我</label>
                        <a href="forget.html" class="text-danger float-right">忘记密码?</a>
                    </div>
                </div>
                <div class="form-group row mt-4">
                    <div class="col-sm-2"></div>
                    <div class="col-sm-10 text-center">
                        <button type="submit" class="btn btn-info text-white form-control">立即登录</button>
                    </div>
                </div>
            </form>
        </div>
    </div>

    <!-- 尾部 -->
    <footer class="bg-dark">
        <div class="container">
            <div class="row">
                <!-- 二维码 -->
                <div class="col-4 qrcode">
                    <img src="https://uploadfiles.nowcoder.com/app/app_download.png" class="img-thumbnail"
                         style="width:136px;"/>
                </div>
                <!-- 公司信息 -->
                <div class="col-8 detail-info">
                    <div class="row">
                        <div class="col">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">关于我们</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">加入我们</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">意见反馈</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">企业服务</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">联系我们</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">免责声明</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link text-light" href="#">友情链接</a>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col">
                            <ul class="nav btn-group-vertical company-info">
                                <li class="nav-item text-white-50">
                                    公司地址：北京市朝阳区大屯路东金泉时代3-2708北京牛客科技有限公司
                                </li>
                                <li class="nav-item text-white-50">
                                    联系方式：010-60728802(电话)&nbsp;&nbsp;&nbsp;&nbsp;admin@nowcoder.com
                                </li>
                                <li class="nav-item text-white-50">
                                    牛客科技©2018 All rights reserved
                                </li>
                                <li class="nav-item text-white-50">
                                    京ICP备14055008号-4 &nbsp;&nbsp;&nbsp;&nbsp;
                                    <img src="http://static.nowcoder.com/company/images/res/ghs.png"
                                         style="width:18px;"/>
                                    京公网安备 11010502036488号
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </footer>
</div>
<script src="https://code.jquery.com/jquery-3.3.1.min.js" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"
        crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" crossorigin="anonymous"></script>
<script th:src="@{/js/global.js}"></script>
<script>
    function refresh_kaptcha(){
        var path = CONTEXT_PATH + "/kaptcha?p=" + Math.random();
        $("#kaptcha").attr("src",path);
    }




</script>
</body>
</html>
```

# 退出登录
- 数据库层在登录中已经设计
- 业务层
```
    public void logout(String ticket) {
		loginTicketMapper.updateStatus(ticket, 1);
		
	}
```
- 控制层
```
    @RequestMapping(path = "/logout", method = RequestMethod.GET)
	public String logout(@CookieValue("ticket") String ticket) {
		userService.logout(ticket);
		return "redirect:/login";
	}
```