# 一般非工具类正规出版物书籍的电子版直接在Kindle商城买就行了，又或者直接上电商渠道购买纸质版，这里只讨论为学术目的使用且不存在便利购买渠道的书籍电子版获取方法。


# 1.Zlibrary（https://z-lib.org/）

禁书，高价原版教科书，史上的名文适用，不推荐使用此网站下载任何国内正规在版出版物。该网站美化十分华丽，每天免费可下10个项目，不过这里多半只有那些比较有名的书、文，如果你想要找冷门的，并不一定能找到你想要的，该网站在大陆已经被wall，一般需要使用scientific surf技术，进去以后直接搜索下载就是了。下面是几张使用截图。

![1](https://user-images.githubusercontent.com/59023098/134794255-4ab2ed35-659d-4815-a0fa-2b244261b32b.PNG)

我这里挂的是韩国镜像站，以《宅兹中国》为例（特此说明：本人并不推荐用该网站下载任何此类在版平价书籍，请使用电商渠道购买纸质版）

![2](https://user-images.githubusercontent.com/59023098/134794258-2edb6944-4d9a-4bda-a0b9-b98e11efbf38.PNG)


搜索后将得到若干结果，在iPad上看建议PDF不容易出错，其他格式用Kybook3也能解码，kindle推荐mobi原生格式,epub,djvu之类格式可以用Calibre转码为mobi（可能出现排版错误）

![3](https://user-images.githubusercontent.com/59023098/134794272-655ddef1-3c03-4ba0-866c-fc7f26e7001e.PNG)


点击下载PDF即可。

# 2.Library Genesis（https://libgen.is/）

毛子的网站，非常强大且简洁，不需要登陆之类的玩意，进去就能搜索而且免费下载。

![4](https://user-images.githubusercontent.com/59023098/134794281-0406a8e5-a260-4ea3-8938-e559b020767a.PNG)


此处以GTM 9为例

![5](https://user-images.githubusercontent.com/59023098/134794288-b4815b96-84c9-410b-9b03-e7a16e2bd8ec.PNG)


在出来的结果中直接点击蓝色书名即可（Introduction to Lie Algebras and Representation Theory）

![6](https://user-images.githubusercontent.com/59023098/134794291-3eec0c16-fd2b-4c81-ba42-e728451c1b55.PNG)


一般直接选择this mirror，再点击Get即可，特殊情况再换源
注意：这里面下载下来的格式不一定是PDF，比如此书下载的是Djvu格式，所以还需要Calibre转个码。

# 3.全国图书馆参考咨询联盟（http://www.ucdrs.superlib.net/）

这里边主要是下载一些古籍之类的，市面上买不到的书。进去以后你会发现没有下载链接：

![7](https://user-images.githubusercontent.com/59023098/134794293-78fac72b-0557-4715-aebc-9e842c26b24e.PNG)

实际上每人每天可以下载50页

这就对了，这就是为啥今天要开一篇文说这件事的原因。首先安装Firefox浏览器，这玩意确实现在已经落伍了但是我只知道用它下这东西的方法，所以Chrome党忍忍吧。
下载之后来到右上角：

![8](https://user-images.githubusercontent.com/59023098/134794295-263dd891-1346-49fe-83c7-2bc229a57920.PNG)


点击三线，打开扩展，搜索Greasemonkey并下载，之后启用该扩展，右上角会出现个猴子：

![9](https://user-images.githubusercontent.com/59023098/134794300-6065a91d-33bd-4b8a-b5ac-012feaf6ddd4.PNG)

然后点击新建脚本，复制粘贴以下内容并保存：

    // ==UserScript==

    // @name			图书互助	

    // @version			2.0.8

    // @include			*search*

    // @include			*bookDetail.jsp?*

    // @include			*advsearch*

    // @include			*book.do?go=guide*

    // @include			*book.do?go=showmorelib*

    // @include			*searchEBook*

    // @include			*www.duxiu.com*

    // @include			*n/jpgfs/book/base*

    // @include			*n/slib/book/slib*

    // @description		方便直接查询全国图书馆参考咨询联盟和各大超星读秀合作图书馆的试读书籍是否可以互助获取全文PDF,可直接自助下载或选择email接收。

    // @copyright		ucdrsebook	

    // @grant			none

    // @namespace ucdrsebook

    // ==/UserScript==

     

    //获取当前网页地址

    //获取当前网页地址

    var myurl = window.location.href;

    //定义统一的样式

    var mystyle = "font-family:Verdana;color:red;font-size:15px;font-weight:bold;";

    	mystyle+="text-align:center;margin-top:5px;margin-bottom:5px;";

     

    app = {

    run: function(){

    	//封面页展示图书显示ssid

    	var isDuxiuIndex=myurl.indexOf("www.duxiu.com")!=-1;

    	if(isDuxiuIndex)

    	{

    		var myul=document.querySelector("ul.zpicImg");

    		var mybooks=myul.querySelectorAll("li");

    		for(var i=0;i<mybooks.length;i++)

    		{

    			var myCov=mybooks[i].querySelector("img").src.toString();

    			var ssid=GetSSID(myCov);

    			var ssNode=CreateSSIDNode2(ssid,"myssid"+i);

    			mybooks[i].appendChild(ssNode);

    		}

    	}

     

    	//搜索页显示ssid

    	var isSearch=myurl.indexOf("search?") != -1;

    	var notBaoku=myurl.indexOf("book/search?")==-1;

    	var notAdvsearch=myurl.indexOf("advsearch") == -1;

    	if (isSearch&&notAdvsearch&&notBaoku) {

    		var subdomain = document.getElementsByName("sp.subdomain")[0];

    		//读秀和长春图书馆的情况

    		//var isDuxiu=subdomain.value == "book.duxiu.com";

    		//var isCcelib=subdomain.value == "book.ly.superlib.net";

            var isDuxiu=myurl.indexOf("book.duxiu.com/search?") != -1;

            var isCcelib=myurl.indexOf("book.ly.superlib.net/search?") != -1;

    		if ( isDuxiu||isCcelib) {

    			//获取书本列表节点

    			var mybooks = document.getElementsByClassName("books");

    			for (var i = 0; i < mybooks.length; i++) {

    				//调整最小显示高度

    				var listDL=mybooks[i].querySelector("dl");

    				listDL.style.minHeight="210px";

    				

    				//获取ssid

    				var ssid=GetSSIDDXID("ssid" + i,"dxid" + i);

    				//创建插入节点

    				var ssNode=CreateSSIDNode2(ssid,"myssid"+i);

    				//插入节点

    				var divImg=mybooks[i].querySelector(".divImg");

     

    				//图书互助

    				var infoAnchor=divImg.querySelector("a").href;

    				var oldstr="bookDetail.jsp?dxNumber=";

    				var newstr="book.do?go=showmorelib&type=1&dxid=";

    				var scgAnchor="https://www.xueshu86.com/ebook/?book_id="+ssid;

    				var csgbutton=document.createElement("a");

    				csgbutton.href=scgAnchor;

    				csgbutton.target="_blank";

    				csgbutton.style="color:green;font-size:15px;font-weight:bold;text-decoration:none;";

    				csgbutton.innerHTML="图书互助";

    				var csgP=document.createElement("p");

    				csgP.style="text-align:center;";

    				csgP.appendChild(csgbutton);

     

    				divImg.appendChild(ssNode);

    				divImg.appendChild(csgP);

    			};

    		}

    		//深圳文献港，全国图书馆联盟搜索页

    		else {

    			var mybooks = document.getElementsByClassName("book1");

    			for (var i = 0; i < mybooks.length; i++) {

    				//获取ssid

    				var ssid=GetSSIDDXID("ssid" + i,"dxid" + i);

    				//创建插入节点

    				var ssNode=CreateSSIDNode2(ssid,"myssid"+i);

     

    				//获取信息页地址

    				var infoUrl=document.getElementById("url"+i).value;

    				var dxid=getValueFromUrl2(infoUrl,"dxNumber");

    				var dValue=getValueFromUrl2(infoUrl,"&d");

    				var myhref="https://www.xueshu86.com/ebook/?book_id=";

    				myhref+=ssid;

    				

    				var csgbutton=document.createElement("a");

    				csgbutton.href=myhref;

    				csgbutton.target="_blank";

    				csgbutton.style="color:green;font-size:15px;font-weight:bold;text-decoration:none;";

    				csgbutton.innerHTML="图书互助";

    				var csgP=document.createElement("p");

    				csgP.style="text-align:center;";

    				csgP.appendChild(csgbutton);

     

    				//插入节点

    				var tdelems = mybooks[i].getElementsByTagName("td");

    				for (var j = 0; j < tdelems.length; j++) {

    					if (tdelems[j].id == "b_img") {

    						var imgNode = tdelems[j];

    						var insertPoint = imgNode.nextSibling;

    						var myParentNode=insertPoint.parentNode;

    						myParentNode.insertBefore(ssNode, insertPoint);

    						myParentNode.insertBefore(csgP,insertPoint);

    					}

    				}

    			}

    		}

    	}

     

    	//信息页面显示ssid

    	if (myurl.indexOf("bookDetail.jsp?") != -1) {

    		//读秀信息页面

    		if (myurl.indexOf("/views/specific/") == -1) {

    			//获取ssid

    			var bookphoto=document.getElementById("bookphoto");

    			var imgsrc=bookphoto.querySelector("img").src;

    			var ssid=GetSSID(imgsrc);

    			//创建插入节点

    			var ssNode=CreateSSIDNode(ssid);

    			var grade1=document.getElementById("grade1");

    			bookphoto.insertBefore(ssNode,grade1);

    			

    			//获取三个按钮的根节点，如果没有，则创建一个

    			var bnt_content=document.querySelector(".bnt_content");

    			if(bnt_content==null)

    			{

    				bnt_content=document.createElement("dd");

    				bnt_content.className="bnt_content";

    				var card_text=document.querySelector(".card_text");

    				var card_dl=card_text.querySelector("dl");

    				card_dl.appendChild(bnt_content);

    			}

    			var bnt_innerHtml=bnt_content.innerHTML;

    			var d=getValueFromUrl("&d");

    			var dxid=getValueFromUrl("dxNumber");

    			/*有待解决d值的问题

    			if(bnt_innerHtml.indexOf("图书馆文献传递")==-1)

    			{

    				var wxcd=document.createElement("a");

    				wxcd.title="功能将您需要的全文发送到您的邮箱！";

    				wxcd.className="bnt_book leftF";

    				var wxcdUrl="javaScript:subtoRefer(true,'/gofirstdrs.jsp?dxNumber=";

    				wxcdUrl+=dxid+"&d="+d+"')";

    				wxcd.href=wxcdUrl;

    				wxcd.innerHTML="图书馆文献传递";

    				if(bnt_innerHtml.indexOf("部分阅读")==-1)

    				{

    					bnt_content.appendChild(wxcd);

    				}

    				else

    				{

    					bnt_content.insertBefore(wxcd,wxcd.firstElementChild);

    				}

    			}

    			*/

    			//部分阅读按钮

    			if(bnt_innerHtml.indexOf("部分阅读")==-1)

    			{

    				var bfydurl="http://book.duxiu.com/readDetail.jsp?dxNumber=";

    				bfydurl+=dxid;

    				bfydurl+="&";

    				bfydurl+="d="+d;

     

    				var bfyd=document.createElement("a");

    				bfyd.href=bfydurl;

    				bfyd.className="bnt_book leftF";

    				bfyd.innerHTML="部分阅读";

    				bnt_content.appendChild(bfyd);

    			}

     

    			//显示查询藏馆按钮

    			var csgbutton=document.createElement("a");

    			var oldstr="bookDetail.jsp?dxNumber=";

    			var newstr="book.do?go=showmorelib&type=1&dxid=";

    			var newAnchor="https://www.xueshu86.com/ebook/?book_id="+ssid;

    			csgbutton.href=newAnchor;

    			csgbutton.className="bnt_book leftF";

    			 csgbutton.style="color:red;font-size:15px;font-weight:bold;text-decoration:none;";

    			csgbutton.innerHTML="图书互助";

    			bnt_content.appendChild(csgbutton);

    		}

    		//深圳文献港,图书馆参考联盟图书信息页

    		else {

    			//获取ssid

    			var tubookimg=document.querySelector(".tubookimg");

    			var imgsrc=tubookimg.querySelector("img").src;

    			var ssid=GetSSID(imgsrc);

    			//创建插入节点

    			var ssNode=CreateSSIDNode(ssid);

    			tubookimg.appendChild(ssNode);

     

    			//显示查询藏馆按钮

    			var csgbutton=document.createElement("a");

    			var dxid=getValueFromUrl("dxNumber");

    			var dvalue=getValueFromUrl("&d");

    			var myhref="https://www.xueshu86.com/ebook/?book_id=";

    			myhref+=ssid;

    			

    			csgbutton.href=myhref;

    			csgbutton.target="_blank";

    			csgbutton.style="color:green;font-size:15px;font-weight:bold;text-decoration:none;";

    			csgbutton.innerHTML="图书互助";

    			var pTemp=document.createElement("p");

    			pTemp.style="text-align:center;";

    			pTemp.appendChild(csgbutton);

    			tubookimg.appendChild(pTemp);

    		}

    	}

     

    	//高级搜索页面显示ssid

    	if (myurl.indexOf("advsearch") != -1) {

    		//定义按钮

    		var btnSSID = document.createElement("input");

    		btnSSID.id = "btnshowSSID";

    		btnSSID.class = "btnInput";

    		btnSSID.type = "button";

    		btnSSID.onclick = showAdvSS;

    		btnSSID.value = "显示SS";

    		btnSSID.style = "width:85px;height:27px;";

     

    		//获取插入点，并插入

    		var searchinfoDiv = document.getElementById("searchinfo");

    		searchinfoDiv.appendChild(btnSSID);

    	}

    	

    	//电子书导航页

    	if(myurl.indexOf("book.do?go=guide")!=-1)

    	{

    		var ulLists=document.getElementsByTagName("ul");

    		var ulBooks=null;

    		for(var i=0;i<ulLists.length;i++)

    		{

    			if(ulLists[i].className=="clearfix")

    			{

    				ulBooks=ulLists[i];

    			}

    		}

    		if(ulBooks!=null)

    		{

    			var bookLists=ulBooks.querySelectorAll("li");

    			for(var j=0;j<bookLists.length;j++)

    			{

    				var ImgDiv=bookLists[j].getElementsByClassName("divImg");

    				if(ImgDiv.length!=0)

    				{

    					var imgNode=ImgDiv[0];

    					var covimgs=imgNode.getElementsByTagName("img");

    					if(covimgs.length!=0)

    					{

    						var covimg=covimgs[0];

    						var imghref=covimg.src;

    						var ssid = GetSSID(imghref);

    						var ssidNode=CreateSSIDNode(ssid);

    						imgNode.appendChild(ssidNode);

    					}

    				}

     

    			}

    		}

    	}

     

    	//电子书检索页

    	if(myurl.indexOf("searchEBook?")!=-1)

    	{

    		var mybooks=document.querySelector(".books");

    		var myBookLists=mybooks.querySelectorAll("li");

    		for(var i=0;i<myBookLists.length;i++)

    		{

    			//调整列表最小高度

    			var listDL=myBookLists[i].querySelector("dl");

    			listDL.style.minHeight="190px";

     

    			//获取ssid

    			var ssid=GetSSIDDXID("ssid" + i,"dxid_" + i);

     

    			//创建插入节点

    			var ssNode=CreateSSIDNode2(ssid,"myssid"+i);

     

    			var divImg=myBookLists[i].querySelector(".divImg");

    			divImg.appendChild(ssNode);

    		}

    	}

    	//藏馆页面

    	if(myurl.indexOf("book.do?go=showmorelib")!=-1)

    	{

    		//显示ssid部分

    		var headDiv=document.querySelector(".header");

    		var flDiv=headDiv.querySelector("img");

    		var imgSrc=flDiv.src;

    		var ssid=GetSSID(imgSrc);

    		var ssidLi=document.createElement("li");

    		ssidLi.style="color:red;font-weight:bold;";

    		console.log(ssid);

    		console.log(ssid.length);

    		if(ssid.length==8)

    		{

    			ssidLi.innerHTML="【SS号】"+ssid;

    		}

    		else

    		{

    			ssidLi.innerHTML="【DX号】"+ssid;

    		}

    		var infoUL=headDiv.querySelector("ul");

    		var insertPoint=infoUL.firstElementChild.nextElementSibling;

    		infoUL.insertBefore(ssidLi,insertPoint);

     

    		//统一按钮风格

    		var btnStyle= "min-width:90px;height:28px;margin-left:10px;font-weight:bold;color:red;";

    		//显示切换按钮

    		var switchButton=document.createElement("input");

    		switchButton.id = "switchSCG";

    		switchButton.type = "button";

    		switchButton.onclick = switchSCG;

    		if(myurl.indexOf("&type=1")!=-1)

    		{

    			switchButton.value = "纸质藏馆";

    		}

    		else

    		{

    			switchButton.value = "图书互助";

    		}

    		switchButton.style = btnStyle;

    		var tabDiv=document.querySelector(".tab");

    		tabDiv.appendChild(switchButton);

     

    		//返回按钮

    		var returnButton=document.createElement("input");

    		returnButton.id="returnBtn";

    		returnButton.type="button";

    		returnButton.style =btnStyle;

    		returnButton.onclick=returnBookDetail;

    		returnButton.value="返回BookDetail";

    		tabDiv.appendChild(returnButton);

     

    		//试读按钮

    		var sd=document.createElement("input");

    		sd.id="sd";

    		sd.type="button";

    		sd.style= btnStyle;

    		sd.value="试读";

    		sd.onclick=sdtz;

    		tabDiv.appendChild(sd);

    	}

     

    	//包库搜索页面显示ssid

    	if(myurl.indexOf("book/search")!=-1)

    	{

    		var ztbg=document.querySelector("div[class='ztbg']");

    		var h2Status=ztbg.querySelector("h2[class='fl zli_t']");

    		var insertPoint=h2Status.nextElementSibling;

    		//定义按钮

    		var btnSSID = document.createElement("input");

    		btnSSID.id = "btnshowSSID";

    		btnSSID.class = "btnInput";

    		btnSSID.type = "button";

    		btnSSID.onclick = GetBaoKuSSID;

    		btnSSID.value = "显示SSID";

    		btnSSID.style = "width:85px;height:30px;color:red;margin-left:15px;";

    		ztbg.insertBefore(btnSSID,insertPoint);

    	}

     

    	//试读页显示封面、书名、版权、封底四个按钮

    	if(myurl.indexOf("/n/jpgfs/book/base/")!=-1)

    	{

    		var jpath="";

    		var mySource=document.querySelector("html").outerHTML;

    		var istart=0;

    		var iend=0;

    		var myIndexStr1="jpgPath:\"";

    		var myIndexStr2="\"";

    		istart=mySource.indexOf(myIndexStr1);

    		istart+=myIndexStr1.length;

    		iend=mySource.indexOf(myIndexStr2,istart);

    		jpath=mySource.substring(istart,iend);

     

    		var baseUrl="http://img.duxiu.com";

    		var myCovUrl=baseUrl+jpath+"cov001?zoom=2";

    		var myBokUrl=baseUrl+jpath+"bok001?zoom=2";

    		var myLegUrl=baseUrl+jpath+"leg001?zoom=2";

    		var myBacUrl=baseUrl+jpath+"cov002?zoom=2";

    		

    		console.log("封面页："+myCovUrl);

    		console.log("书名页："+myBokUrl);

    		console.log("版权页："+myLegUrl);

    		console.log("封底页："+myBacUrl);

     

    		var t_content=document.querySelector("#t_content");

    		t_content.style="width:815px;";

    		var tc_right=document.querySelector("#tc_right");

    		tc_right.style="width:240px;";

    		var myul=tc_right.querySelector("ul");

     

    		var cov001li=addALink(myCovUrl,"cov001","封面","cov001.pdg");

    		cov001li.style.marginTop="7px";

    		myul.appendChild(cov001li);

     

    		var bok001li=addALink(myBokUrl,"bok001","书名","bok001.pdg");

    		bok001li.style.marginTop="7px";

    		myul.appendChild(bok001li);

     

    		var leg001li=addALink(myLegUrl,"leg001","版权","leg001.pdg");

    		leg001li.style.marginTop="7px";

    		myul.appendChild(leg001li);

     

    		var cov002li=addALink(myBacUrl,"cov002","封底","cov002.pdg");

    		cov002li.style.marginTop="7px";

    		myul.appendChild(cov002li);

     

    		var oneKeyDown=document.createElement("li");

    			oneKeyDown.style="margin-top: 7px;margin-left:6px;";

    		var oneKeyDownlink=document.createElement("a");

    			oneKeyDownlink.id="oneKeyDown";

    			oneKeyDownlink.style="color: red;font-weight:bold;cursor: pointer;";

    			oneKeyDownlink.innerHTML="一键下载";

    			oneKeyDownlink.href="#";

    			oneKeyDownlink.onclick=OneKeyDownAll;

    		oneKeyDown.appendChild(oneKeyDownlink);

    		myul.appendChild(oneKeyDown);

    	}

     

    	//包库在线阅读页显示封面、书名、版权、封底四个按钮

    	if(myurl.indexOf("/n/slib/book/slib/")!=-1)

    	{

    		var jpath="";

    		var mySource=document.querySelector("html").outerHTML;

    		var istart=0;

    		var iend=0;

    		var myIndexStr1="jpgPath: \"";

    		var myIndexStr2="\"";

    		istart=mySource.indexOf(myIndexStr1);

    		istart+=myIndexStr1.length;

    		iend=mySource.indexOf(myIndexStr2,istart);

    		jpath=mySource.substring(istart,iend);

    		console.log(jpath);

    		var baseUrl="http://img.sslibrary.com";

    		var myCovUrl=baseUrl+jpath+"cov001?zoom=2";

    		var myBokUrl=baseUrl+jpath+"bok001?zoom=2";

    		var myLegUrl=baseUrl+jpath+"leg001?zoom=2";

    		var myBacUrl=baseUrl+jpath+"cov002?zoom=2";

    		

    		console.log("封面页："+myCovUrl);

    		console.log("书名页："+myBokUrl);

    		console.log("版权页："+myLegUrl);

    		console.log("封底页："+myBacUrl);

     

    		var ToolsBar=document.querySelector(".ToolsBar");

    		var myul=ToolsBar.querySelector("ul");

    		myul.style.width="1366px";

     

     

    		var cov001li=addALink(myCovUrl,"cov001","封面","cov001.pdg");

    		myul.appendChild(cov001li);

     

    		var bok001li=addALink(myBokUrl,"bok001","书名","bok001.pdg");

    		myul.appendChild(bok001li);

     

    		var leg001li=addALink(myLegUrl,"leg001","版权","leg001.pdg");

    		myul.appendChild(leg001li);

     

    		var cov002li=addALink(myBacUrl,"cov002","封底","cov002.pdg");

    		myul.appendChild(cov002li);

     

    		var oneKeyDown=document.createElement("li");

    			oneKeyDown.style="margin-left:6px;";

    		var oneKeyDownlink=document.createElement("a");

    			oneKeyDownlink.id="oneKeyDown";

    			oneKeyDownlink.style="color: red;font-weight:bold;cursor: pointer;";

    			oneKeyDownlink.innerHTML="一键下载";

    			oneKeyDownlink.href="#";

    			oneKeyDownlink.onclick=OneKeyDownAll;

    		oneKeyDown.appendChild(oneKeyDownlink);

    		myul.appendChild(oneKeyDown);

    	}

    }};

     

     

    function GetBaoKuSSID()

    {

    	var myssids=document.querySelectorAll("#myssid");

    	if(myssids.length!=0)

    	{

    		return;

    	}

    	else

    	{

    		var mybooklist=document.querySelectorAll("ul[class='clearfix zli_item']");

    		for(var i=0;i<mybooklist.length;i++)

    		{

    			var mybook=mybooklist[i].querySelector("li[class='fl zli_img']");

    			var bookimg=mybook.querySelector("img");

    			var myimgSrc=bookimg.src;

    			console.log(myimgSrc);

    			var myssid=GetSSID(myimgSrc);

    			console.log(myssid);

    			var ssidNode=CreateSSIDNode(myssid);

    			mybook.appendChild(ssidNode);

    		}

    	}

    }

     

    function OneKeyDownAll()

    {

    	var mylinksId=new Array("cov001","bok001","leg001","cov002");

    	for(var i=0;i<mylinksId.length;i++)

    	{

    		var mylink=document.getElementById(mylinksId[i]);

    		mylink.click();

    	}

    }

     

    function addALink(urlStr,myIdStr,innerHTMLStr,downloadName)

    {

    	var myli=document.createElement("li");

    	myli.style="margin-left:6px;";

    	var alink=document.createElement("a");

    	alink.id=myIdStr;

    	alink.innerHTML=innerHTMLStr;

    	alink.href=urlStr;

    	alink.style="color: green;font-weight:bold;cursor: pointer;";

    	alink.download=downloadName;

    	myli.appendChild(alink);

    	return myli;

    }

     

    //切换藏书查询

    function switchSCG()

    {

    	var newurl="";

    	if(myurl.indexOf("&type=1")!=-1)

    	{

    		newurl=myurl.replace("&type=1","");

    	}

    	else

    	{

    		newurl=myurl+"&type=1";

    	}

    	window.location.href=newurl;

    }

     

     

    //跳转试读页

    function sdtz()

    {

    	var d=getValueFromUrl("&d");

    	var dxid=getValueFromUrl("&dxid");

    	newurl="http://book.duxiu.com/readDetail.jsp?dxNumber=";

    	newurl+=dxid;

    	newurl+="&";

    	newurl+="d="+d;

    	window.open(newurl,"_blank");

    }

     

    //返回bookdetail

    function returnBookDetail()

    {

    	var d=getValueFromUrl("&d");

    	var dxid=getValueFromUrl("&dxid");

    	newurl="http://book.duxiu.com/bookDetail.jsp?dxNumber=";

    	newurl+=dxid;

    	newurl+="&";

    	newurl+="d="+d;

    	window.location.href=newurl;

    }

    //从当前网址中提取某个字段，输入字段名称

    function getValueFromUrl(myfield)

    {

    	var str=myfield+"=";

    	if(myurl.indexOf(str)!=-1)

    	{

    		var reg =new RegExp(myfield+"\\=\\w+");

    		

    		var fieldStr = myurl.match(reg)[0];

    		console.log(myfield.toString());

    		var fieldValue = fieldStr.replace(myfield+"=", "");

    		return fieldValue;

    	}

    }

     

    //从当前网址中提取某个字段，输入字段名称

    function getValueFromUrl2(URL,myfield)

    {

    	var str=myfield+"=";

    	if(URL.indexOf(str)!=-1)

    	{

    		var reg =new RegExp(myfield+"\\=\\w+");

    		

    		var fieldStr = URL.match(reg)[0];

    		var fieldValue = fieldStr.replace(myfield+"=", "");

    		return fieldValue;

    	}

    }

     

    //获取ssid或者dxid，当ssid不存在的时候，返回dxid

    //输入ssid的元素id以及读秀dxid的元素id

    function GetSSIDDXID(ssidNodeID,dxidNodeID)

    {

    	//获取ssid

    	var ssid=GetSSIDByID(ssidNodeID,"value");

     

    	//获取dxid

    	var dxid=GetSSIDByID(dxidNodeID,"value");

    	

    	//如果ssid不存在，则用dxid替代

    	if (ssid == "") {

    		ssid = dxid;

    	}

    	return ssid;

    }

    //获取ssid，输入元素的id、属性名称（一般为value）

    function GetSSIDByID(elementID,strAttribute)

    {

    	var ssidNode=document.getElementById(elementID);

    	var ssid=ssidNode.getAttribute(strAttribute);

    	return ssid;

    }

    //创建默认的ssid节点，节点id为myssid

    function CreateSSIDNode(ssid)

    {

    	var myid='myssid';

    	return CreateSSIDNode2(ssid,myid);

    }

    //创建ssid节点，输入ssid和节点id

    function CreateSSIDNode2(ssid,strID)

    {

    	var ssNode = document.createElement("p");

    	ssNode.id=strID;

    	ssNode.style=mystyle;

    	ssNode.innerHTML=ssid;

    	return ssNode;

    }

     

    //高级搜索页面显示ssid

    function showAdvSS() {

    	//获取图书节点

    	var mybooks = document.getElementsByClassName("books")[0];

    	var booklists=mybooks.getElementsByTagName("li");

    	for (var i = 0; i < booklists.length; i++) {

    		//判断是否存在，如果存在，则跳过

    		var myssid = document.getElementById("myssid" + i);

    		if (myssid != null) {

    			continue;

    		}

    		//获取ssid

    		var ssid=GetSSIDDXID("ssid" + i,"dxid" + i);

     

    		//创建插入节点

    		var ssNode=CreateSSIDNode2(ssid,"myssid"+i);

     

    		//修改dl最低高度

    		var listDL=booklists[i].querySelector("dl");

    		listDL.style.minHeight="210px";

     

    		//插入数据

    		var divImg=booklists[i].getElementsByClassName("divImg")[0];

     

    		var infoAnchor=divImg.querySelector("a").href;

    		var oldstr="bookDetail.jsp?dxNumber=";

    		var newstr="book.do?go=showmorelib&type=1&dxid=";

    		var scgAnchor="https://www.xueshu86.com/ebook/?book_id="+ssid;

    		//图书互助

    		var csgbutton=document.createElement("a");

    		csgbutton.href=scgAnchor;

    		csgbutton.target="_blank";

    		csgbutton.style="color:green;font-size:15px;font-weight:bold;text-decoration:none;";

    		csgbutton.innerHTML="图书互助";

    		var csgP=document.createElement("p");

    		csgP.style="text-align:center;";

    		csgP.appendChild(csgbutton);

     

    		divImg.appendChild(ssNode);

    		divImg.appendChild(csgP);

    	}

    }

     

    function GetSSID(strImgSrc) {

    	var ssid = "";

        var iidStr=GetEncode(strImgSrc);

        var ssidStr = DeCode(iidStr);

        ssid = TrimString(ssidStr);

        return ssid;

    }

     

    function GetEncode(strImgSrc) {

        var reg = /iid\=\w+/;

        var iidStr = strImgSrc.match(reg)[0];

        iidStr = iidStr.replace("iid=", "");

        return iidStr;

    }

     

    function TrimString(inputStr) {

        var outPutStr = "";

        inputStr = inputStr.replace(/\//g, "");

        var reg = /\d{8,}/;

    	outPutStr = inputStr.match(reg);

    	outPutStr=outPutStr.toString();

        return outPutStr;

    }

     

    function DeCode(EnCodeStr) {

        var decodeStr = "";

        var baseNumStr = EnCodeStr.substring(EnCodeStr.length - 2);

        var baseNum = parseInt(baseNumStr, 16);

        var myCodeStr = EnCodeStr.substring(0, EnCodeStr.length - 16);

        for (var i = 0; i < myCodeStr.length; i = i + 2) {

            decodeStr += GetSubString(myCodeStr, baseNum, i);

        }

        return decodeStr;

    }

     

    function GetSubString(EnCodeStr, BaseNum, startIndex) {

        var s = "";

        s = EnCodeStr.substring(startIndex, startIndex + 2);

        //转换进制

        var i = parseInt(s, 16) - BaseNum;

        s = String.fromCharCode(i);

        return s;

    }

     

    try {

    	app.run();

    } catch (e) {

    	console.log(e);

    }

然后重启Firefox，再回去就会发现多了一个功能：图书互助

![10](https://user-images.githubusercontent.com/59023098/134794311-6f731b2d-1797-4c3c-aaac-44167476332f.PNG)


点击，接下来按照它页面上的提示来傻瓜式操作即可，这个脚本是要付费使用的，下载一本书是2元，这2元实际上是脚本提供方用多个邮箱给你跑50页50页抓取所有页面再打包发给你的成本。

