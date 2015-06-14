# coldfusion-TinyPNG
TinyPNG compression in ColdFusion

<cfscript>
	try {
		LOCAL = StructNew();
		LOCAL.filePath = "";
		LOCAL.apiKEY = ToBase64("XXXXXXXXX");
		LOCAL.httpService = new http();
		LOCAL.httpService.setMethod("post");
		LOCAL.httpService.setCharset("utf-8");
		LOCAL.httpService.setUseragent("Mozilla/5.0 (Windows NT 6.2; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.45 Safari/537.36");
		LOCAL.httpService.setUrl("https://api.tinify.com/shrink");
		LOCAL.httpService.addParam(type="header",name="Authorization",value="Basic #LOCAL.apiKEY#");
		LOCAL.httpService.addParam(type="body",value="#FileReadBinary(LOCAL.filePath)#");
		LOCAL.result = LOCAL.httpService.send().getPrefix();
		LOCAL.httpService.clearParams();
		writedump(LOCAL.result);
	} catch (any e) {
		writedump(e);
	}
</cfscript>
