#Wiki Notes Markdown文档展示

[Wiki Notes](http://wikinotes.jingapps.com/) 是一个纯Markdown文档展示程序, 一个用于展示你的说明文档、电子书、代码片段、ideas等的地方。

![logo](images/logo.jpg)

日常工作中时常书写文档并且需要在web端展示出来, 而它往往不同于博客, 它专注于纯文本的书写方式, 这里采用了Markdown 格式。

##目录与正文

1. 根目录下的 `sidebar.md` 为目录所展示的内容, 你需要手工去维护这个目录与正文的对应关系。

2. 根目录下的 `docs` 目录为文档文件存放目录, 文档名称需要与目录文件中的路径文成一致, 例如:

		sidebar.md 
		
			[Wiki Notes 介绍](#docs/intro)
			[Wiki Notes 使用](#docs/usage)
			
		目录对应文件:
		
		/docs/intro.md
		/docs/usage.md
	
3. 根目录下的 `README.md` 为默认的前言文件。

4. 文档中嵌入的图片均放到 `images` 目录中并在页面嵌入:

		![logo](images/logo.jpg)

##基本配置

1. 配置页面显示元素

	在 `js/ditto.js` 中通过修改以下内容来控制页面中是否( `true` / `false` )显示
	
		// display elements
	    sidebar: true, //是否显示目录
	    edit_button: true, //是否显示编辑按钮
	    back_to_top_button: true, //是否显示返回顶部按钮
	    save_progress: true, // 保存阅读进度
	  
2. 配置DISQUS评论组件

	DISQUS是流行的第三方社会化评论组件,可以方便的嵌入到页面中, 需要先移步 [disqus.com](https://disqus.com/) 进行注册和新增站点
	
	在 `js/ditto.js` 中通过修改以下内容来嵌入DISQUS：
	
		// 加载disqus
        (function() {
        		//[1]配置DISQUS站点对应的shortname
            window.disqus_shortname = 'wiki-notes';
            window.disqus_identifier = (location.hash ? location.hash.replace("#", "") : 'READEME');
            window.disqus_title = $(ditto.content_id + " h1").text();
            //[2]配置评论对应的页面链接
            window.disqus_url = 'http://wikinotes.jingapps.com/' + (location.hash ? location.hash.replace("#", "") : 'README');

            (function() {
                var dsq = document.createElement('script');
                dsq.type = 'text/javascript';
                dsq.async = true;
                dsq.src = 'http://' + window.disqus_shortname + '.disqus.com/embed.js';
                (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
            })();
        })();		

3. 配置编辑功能

	如果是私有文档, 请修改 `配置1` 中的 `edit_button: false` , 即隐藏修改按钮
	
	如果是公共文档并且程序源码和文档托管在 `github`, 则需要修改 `index.html` 入口文件中的:
	
		ditto.base_url = "https://github.com/JingwenTian/wikinotes/edit/master"; //修改页的链接
		
	以供阅读者可以通过 `fork` 你的源码进行修改。
	
##开始你的旅程

配置好后就可以开始你的写作之旅了, 只需要将Markdown 文档放在 `docs` 目录下并且在 目录文件 中做好映射关系就好了!

Enjoy it!

---

##关于Gitbook

`GitBook` 是一个命令行工具（Node.js库），我们可以借用该工具使用 `Github/Git` 和 `Markdown` 来制作精美的图书.

`wikinotes` 就是参考了 `gitbook` 的形式当然只是个人应用记录文档的工具. 如果你想通过 `git/markdown` 来写作推荐你使用 [gitbook](https://github.com/GitbookIO/gitbook) 

**使用方法如下:**

1. 通过 `npm` 安装

	$ npm install gitbook-cli -g
	
2. 创建目录和 `SUMMARY.md` 文件(目录文件) 然后执行命令初始化
	
	gitbook init

此时就已经已经按照目录文件生成了目录结构

3. You can serve a repository as a book using:

	gitbook serve ./repository
	
   Or simply build the static website using:
   
   	gitbook build ./repository ./outputFolder

		
