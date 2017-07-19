## Install Alexa in Linux

1. Ubuntu 14.04  
2. 安裝 vlc  
`% sudo apt-get update`  
`% sudo apt-get install vlc browser-plugin-vlc`
3.  設定 vlc
	修改環境變數:  
		% sudo vim ~/.bashrc   ##文件的末尾追加下面內容:  
		export LD_LIBRARY_PATH="/usr/lib/vlc"  
		export VLC_PLUGIN_PATH="/usr/lib/vlc/plugins"  
	使環境變量馬上生效 :  
		% source ~/.bashrc  
4. 安裝 jdk , 直接下載jdk壓縮包方式安裝, (http://www.cnblogs.com/a2211009/p/4265225.html)  
	a. 分為下面5個步驟 :  
   			1.官網下載JDK  
   			2.解壓縮,放到指定目錄  
   			3.配置環境變量  
   			4.設置系統默認JDK  
　			5. 測試jdk  
	b. 官網下載JDK  
		http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html  
	c. sudo  mkdir /usr/lib/jvm  
	d. sudo  tar -zxvf jdk-8u111-linux-x64.tar.gz -C /usr/lib/jvm  
	e. 修改環境變數 :   
		% sudo vim ~/.bashrc  ##文件的末尾追加下面內容:  
			export JAVA_HOME="/usr/lib/jvm/jdk1.8.0_111"  
			export JRE_HOME="${JAVA_HOME}/jre"  
			export CLASSPATH=".:${JAVA_HOME}/lib:${JRE_HOME}/lib"  
			export PATH="${JAVA_HOME}/bin:$PATH"  
	f. 使環境變量馬上生效 :   
		% source ~/.bashrc  
	g. % echo $JRE_HOME #查詢環境變數  
	h. 設置系統默認jdk 版本  
		sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_111/bin/java 300  
		sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_111/bin/javac 300  
		sudo update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/jdk1.8.0_111/bin/jar 300  
		sudo update-alternatives --install /usr/bin/javah javah /usr/lib/jvm/jdk1.8.0_111/bin/javah 300  
		sudo update-alternatives --install /usr/bin/javap javap /usr/lib/jvm/jdk1.8.0_111/bin/javap 300  
	i. 然後執行:  
		sudo update-alternatives --config java  
		若是初次安裝jdk,會有下面的提示 :   
		There is only one alternative in link group java (providing /usr/bin/java): /usr/lib/jvm/jdk1.8.0_111/bin/java  
		Nothing to configure.  
	j. 測試jdk  
		java -version   
				java version "1.8.0_111"  
				Java(TM) SE Runtime Environment (build 1.8.0_111-b14)  
				Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)  
5. 安裝  Maven  
	a. nsure JAVA_HOME environment variable is set and points to your JDK installation  
	b. tar xzvf apache-maven-3.3.9-bin.tar.gz  
	c. 修改環境變數 :   
			% sudo vim ~/.bashrc  ##文件的末尾追加下面內容:  
				export PATH="/home/jazzhipster/Desktop/other_pkg/apache-maven-3.3.9/bin:$PATH"  
	d. 使環境變量馬上生效 :   
			% source ~/.bashrc  
	e. 測試 mvn  有無安裝成功  
			% mvn -v  #會顯示如下  
			Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-11T00:41:47+08:00)  
			Maven home: /home/jazzhipster/Desktop/other_pkg/apache-maven-3.3.9  
			Java version: 1.8.0_111, vendor: Oracle Corporation  
			Java home: /usr/lib/jvm/jdk1.8.0_111/jre  
			Default locale: en_US, platform encoding: UTF-8  
			OS name: "linux", version: "4.2.0-27-generic", arch: "amd64", family: "unix"  
6. Generating Self Signed Certificates  
	a. apt-get, to install OpenSSL.  
	b. Edit the {REFERENCE_IMPLEMENTATION}/samples/javaclient/ssl.cnf  
			1. 填入	countryName             = US                 				# C=  
			2. 填入 LINUX 的 IP :   
					IP.3	= 192.168.0.103  
	c. 執行 ..../samples/javaclient/generate.sh  
		1. 輸入 Product ID: my_device  
				Serial Number : 123456  
				Password for keystores : android  
	d. 修改 ..../samples/javaclient/config.json
		1. 	"sslKeyStore":"/home/jazzhipster/Desktop/alexa-avs-sample-app-master/samples/javaclient/certs/server/jetty.pkcs12",  
        2.	"sslKeyStorePassphrase":"android",  
        3.	"sslClientKeyStore":"/home/jazzhipster/Desktop/alexa-avs-sample-app-master/samples/javaclient/certs/client/client.pkcs12",  
        4.	"sslClientKeyStorePassphrase":"android",  
        5.	"sslCaCert":"/home/jazzhipster/Desktop/alexa-avs-sample-app-master/samples/javaclient/certs/ca/ca.crt"  
		6.  "productId":"my_device",  
    	7.	"dsn":"123456",  
	e. 修改 /samples/javaclient/pom.xml  
		1. {alpn-boot.version}xxx{/alpn-boot.version}   
				xxx : 填入 8.1.9.v20160720  
7. 到 ..../samples/javaclient 目錄下 :  
	a. mvn clean  
	b. mvn validate  
	c. mvn install  
	d. mvn exec:exec  
8. 將 ....\samples\javaclient\certs\ca\ca.crt  
   copy 到  ....\samples\androidCompanionApp\app\src\main\res\raw\ca.crt 下  
9. android 手機 version 要大於 5.1.0  







