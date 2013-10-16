---
layout: post
title: Bing translator API
categories:
- IT
tags:
- translate
- Bing
---

使用exitwp把从WordPress导出的XML文件转换成MD文件之后，所有MD文件的文件名都是乱码。有个解决方案可以解决这个文件名的问题，从MD文件的title属性中把原来文章的中文标题读出来赋给文件名，不过jekyll系统对中文文件名支持的不是那么好，所以需要转换这些中文文件名为英文。Bing Translator登场。
<br/>



###注册Windows Azure用户###
[https://datamarket.azure.com/][1]
<br/>

###订阅Microsoft Translator API###
[http://blogs.msdn.com/b/translation/p/gettingstarted1.aspx][2]
<br/>

###Using the Client ID and Client Secret to get the Access Token###
    //AdmAcessToken class
    public class AdmAccessToken
    {
        public string access_token { get; set; }
        public string token_type { get; set; }
        public string expires_in { get; set; }
        public string scope { get; set; }
    }
    
    //Get Access Token Method
    public string GetAccessToken()
    {
		string clientID = "<Your Client ID>";
		string clientSecret = "<Your Client Secret>";

		String strTranslatorAccessURI = "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13";
		String strRequestDetails = string.Format("grant_type=client_credentials&client_id={0}&client_secret={1}&scope=http://api.microsofttranslator.com", HttpUtility.UrlEncode(clientID), HttpUtility.UrlEncode(clientSecret));

		System.Net.WebRequest webRequest = System.Net.WebRequest.Create(strTranslatorAccessURI);
		webRequest.ContentType = "application/x-www-form-urlencoded";
		webRequest.Method = "POST";

		byte[] bytes = System.Text.Encoding.ASCII.GetBytes(strRequestDetails);
		webRequest.ContentLength = bytes.Length;
		using (System.IO.Stream outputStream = webRequest.GetRequestStream())
		{
			outputStream.Write(bytes, 0, bytes.Length);
		}
		System.Net.WebResponse webResponse = webRequest.GetResponse();
		System.Runtime.Serialization.Json.DataContractJsonSerializer serializer = new System.Runtime.Serialization.Json.DataContractJsonSerializer(typeof(AdmAccessToken));
		
		//Get deserialized object from JSON stream 
		AdmAccessToken token = (AdmAccessToken)serializer.ReadObject(webResponse.GetResponseStream());

		string appID = "Bearer " + token.access_token;
        return appID;
        }
    
###Add soap service reference###
http://api.microsofttranslator.com/V2/Soap.svc
    ServiceReference1.LanguageServiceClient client = new ServiceReference1.LanguageServiceClient();
    string englishName = client.Translate(appID, "中文内容", "zh-cn", "en-us", "text/html", "general");

<br/>
<br/>
> Written with [StackEdit](http://benweet.github.io/stackedit/).


  [1]: https://datamarket.azure.com/
  [2]: http://blogs.msdn.com/b/translation/p/gettingstarted1.aspx