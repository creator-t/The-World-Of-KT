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
