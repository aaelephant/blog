###ios app接入unity工程步骤
1. Unity导出新的工程后，把新的xcode工程中的代码全部替换到旧工厂中，在替换之前，保存好：	```
	Assets_RN、Bridge、Classes（app的）、Classes/Prefix.pch、
		```
				```
	Classes/UnityAppController.h、Classes/UnityAppController.mm
		```
				```
	Classes/UI/UnityAppController+ViewHanding.h、
			```
			```	Classes/UI/UnityAppController+ViewHanding.mm
						```
							```
	Classes/UI/UnityViewControllerBaseiOS.h、
			```		```	Classes/UI/UnityViewControllerBaseiOS.mm
					```		```
	Libraries/Plugins/iOS/MediaPlayer、	Libraries/Plugins/iOS/WhaleyVR
			```	

2. 删除Frameworks/Plugins/iOS/MediaPlayer、Libraries/Plugins/iOS/MediaPlayer/iOSPluginInterface.m
3. 最后重新添加资源文件

###接入过程中遇到的问题
* UnityInitApplicationNoGraphics(…)处crash是Data文件夹没有编译到工程中，删除文件夹，重新拖拽。