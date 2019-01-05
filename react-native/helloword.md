##RN集成开源库三步
1.npm install react-native-fetch-blob --save

2.react-native link react-native-fetch-blob

3.重新run ios 或 android ，因为link到库后，原生代码有更新

4.Xcode 10: third-party: 'config.h' file not found
解决方法："react": "16.6.3",
    "react-native": "0.57.8",把这两个升级到最新
