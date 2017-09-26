# redEyeBookMarkPlugin
How to use Plugin:
**Note -> See this sample Demo application (https://github.com/redEyeProgrammer/PluginSampleApplication.git) that uses myHybridPlugin and configure your testApp accordingly

 Create a test application from Terminal (testApp would consume this Plugin)

cordova create testapp com.redEye.testapp TestApp (use your bundleIdentifier of choice)
cd testapp

cordova plugin add cordova-plugin-add-swift-support --save (plugin that will install the bridging header for Swift files)

cordova platform add ios

cordova build ios

Open ProjectWorkspace and do the following. Create a storyboard name Main
Make Main Storyboard the Main interface in Project settings
Open Main Storyboard and Create TabBarController
Create a tableViewController class
Make first item of tabBarController inherit MainViewController (that came pre-added)
Make Second item inherit tableViewController (and make the VC in storyboard a TableViewController)


**Note -> See this sample Demo application (https://github.com/redEyeProgrammer/PluginSampleApplication.git) that uses myHybridPlugin and configure your testApp accordingly
