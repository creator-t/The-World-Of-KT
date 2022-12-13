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

